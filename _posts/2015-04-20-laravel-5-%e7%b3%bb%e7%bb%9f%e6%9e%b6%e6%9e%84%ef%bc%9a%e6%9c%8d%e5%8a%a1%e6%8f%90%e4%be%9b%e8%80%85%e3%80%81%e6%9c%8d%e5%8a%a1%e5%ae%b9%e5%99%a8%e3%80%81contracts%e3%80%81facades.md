---
ID: 644877
post_title: >
  Laravel 5
  系统架构：服务提供者、服务容器、Contracts、Facades
author: 南 靖男
post_date: 2015-04-20 17:15:19
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2015/04/644877
published: true
---
<a href="http://laravel-china.org/docs/5.0/">官方文档</a>在一方面真的写的很糟糕，完全没描述相互之间的关系。

事实上，<a href="http://laravel-china.org/docs/5.0/providers">服务提供者（Service Provider）</a>、<a href="http://laravel-china.org/docs/5.0/container">服务容器（Service Container）</a>、<a href="http://laravel-china.org/docs/5.0/contracts">Contracts</a>、<a href="http://laravel-china.org/docs/5.0/facades">Facades</a> 是一件东西的多个方面。其实就是 Yii 的组件（Component）。

和 Yii 一样，Laravel 的所有功能都是通过与 Yii 组件类似的服务架构来实现的。

一个最简单直接的例子是 <a href="https://packagist.org/packages/illuminate/hashing">Lavarel Hashing</a> 服务。其自身只是一个 <a href="http://php.net/manual/zh/function.password-hash.php">Bcrypt hash</a> 的封装。

首先，Laravel 5 定义了一个 Contracts：<code>Illuminate/Contracts/Hashing/Hasher.php</code>
<pre lang="PHP">
<?php namespace Illuminate\Contracts\Hashing;
interface Hasher {
	/**
	 * Hash the given value.
	 *
	 * @param  string  $value
	 * @param  array   $options
	 * @return string
	 */
	public function make($value, array $options = array());
	/**
	 * Check the given plain value against a hash.
	 *
	 * @param  string  $value
	 * @param  string  $hashedValue
	 * @param  array   $options
	 * @return bool
	 */
	public function check($value, $hashedValue, array $options = array());
	/**
	 * Check if the given hash has been hashed using the given options.
	 *
	 * @param  string  $hashedValue
	 * @param  array   $options
	 * @return bool
	 */
	public function needsRehash($hashedValue, array $options = array());
}
</pre>

Contracts 只是描述一个服务的具体方法，而不是实现该服务。Container 才是服务的具体实现，对于一个服务来说，可能会有多种不同的实现。Hash 目前只有一个，就是：<code>Illuminate/Hashing/BcryptHasher.php</code>
<pre lang="PHP">
<?php namespace Illuminate\Hashing;
use RuntimeException;
use Illuminate\Contracts\Hashing\Hasher as HasherContract;
class BcryptHasher implements HasherContract {
	/**
	 * Default crypt cost factor.
	 *
	 * @var int
	 */
	protected $rounds = 10;
	/**
	 * Hash the given value.
	 *
	 * @param  string  $value
	 * @param  array   $options
	 * @return string
	 *
	 * @throws \RuntimeException
	 */
	public function make($value, array $options = array())
	{
		$cost = isset($options['rounds']) ? $options['rounds'] : $this->rounds;
		$hash = password_hash($value, PASSWORD_BCRYPT, array('cost' => $cost));
		if ($hash === false)
		{
			throw new RuntimeException("Bcrypt hashing not supported.");
		}
		return $hash;
	}
	/**
	 * Check the given plain value against a hash.
	 *
	 * @param  string  $value
	 * @param  string  $hashedValue
	 * @param  array   $options
	 * @return bool
	 */
	public function check($value, $hashedValue, array $options = array())
	{
		return password_verify($value, $hashedValue);
	}
	/**
	 * Check if the given hash has been hashed using the given options.
	 *
	 * @param  string  $hashedValue
	 * @param  array   $options
	 * @return bool
	 */
	public function needsRehash($hashedValue, array $options = array())
	{
		$cost = isset($options['rounds']) ? $options['rounds'] : $this->rounds;
		return password_needs_rehash($hashedValue, PASSWORD_BCRYPT, array('cost' => $cost));
	}
	/**
	 * Set the default password work factor.
	 *
	 * @param  int  $rounds
	 * @return $this
	 */
	public function setRounds($rounds)
	{
		$this->rounds = (int) $rounds;
		return $this;
	}
}
</pre>

除了实现 Contracts 中定义的三个方法外，还实现了一个额外 <code>setRounds()</code> 方法。

下一步就是注册为服务提供者了：<code>Illuminate/Hashing/HashServiceProvider.php</code>
<pre lang="PHP">
<?php namespace Illuminate\Hashing;
use Illuminate\Support\ServiceProvider;
class HashServiceProvider extends ServiceProvider {
	/**
	 * Indicates if loading of the provider is deferred.
	 *
	 * @var bool
	 */
	protected $defer = true;
	/**
	 * Register the service provider.
	 *
	 * @return void
	 */
	public function register()
	{
		$this->app->singleton('hash', function() { return new BcryptHasher; });
	}
	/**
	 * Get the services provided by the provider.
	 *
	 * @return array
	 */
	public function provides()
	{
		return array('hash');
	}
}
</pre>

很明显的 register 了服务，具体做的就是 new 了一个 Container。如果容器有多种实现，这时建议使用 Config 来配置服务了。
<pre lang="PHP">
$this->app->singleton('hash', function($app) { return new Hasher($app['config']['hash']); });
</pre>

这时候 Hasher 实际上一个工厂类（Factory），使用配置来确定具体的，如 <code>new Hasher('bcrypt')</code> 来实例化。

如果服务要延迟载入，也就是按需载入。需要有一个激活标志，也就是 <code>provides()</code> 方法。

当然，<code>HashServiceProvider.php</code> 必须在 <code>config/app.php</code> 的 <code>providers</code> 中定义 <code>'Illuminate\Hashing\HashServiceProvider'</code> 行。

这时，就可以使用：
<pre lang="PHP">
$this->app->make('hash')->make('password');
$this->app['hash']->make('password');
</pre>

最后，声明一个 Facade：<code>Illuminate/Support/Facades/Hash.php</code>
<pre lang="PHP">
<?php namespace Illuminate\Support\Facades;
/**
 * @see \Illuminate\Hashing\BcryptHasher
 */
class Hash extends Facade {
	/**
	 * Get the registered name of the component.
	 *
	 * @return string
	 */
	protected static function getFacadeAccessor()
	{
		return 'hash';
	}
}
</pre>

在 <code>config/app.php</code> 的 <code>aliases</code> 中定义 <code>'Hash' => 'Illuminate\Support\Facades\Hash'</code> 行。

那么，就不用上面长长的 <code>$this->app->make('hash')</code>，直接：
<pre lang="PHP">
Hash::make('password');
</pre>