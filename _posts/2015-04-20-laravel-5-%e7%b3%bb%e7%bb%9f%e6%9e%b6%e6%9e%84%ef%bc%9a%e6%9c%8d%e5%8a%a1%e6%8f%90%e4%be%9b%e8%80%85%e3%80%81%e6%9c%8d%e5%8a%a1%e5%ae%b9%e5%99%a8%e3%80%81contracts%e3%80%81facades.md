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
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:3795:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">namespace</span> Illuminate\Contracts\Hashing<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">interface</span> Hasher <span style="color: #009900;">&#123;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Hash the given value.
    *
    * @param  string  $value
    * @param  array   $options
    * @return string
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> make<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Check the given plain value against a hash.
    *
    * @param  string  $value
    * @param  string  $hashedValue
    * @param  array   $options
    * @return bool
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> check<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> <span style="color: #000088;">$hashedValue</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Check if the given hash has been hashed using the given options.
    *
    * @param  string  $hashedValue
    * @param  array   $options
    * @return bool
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> needsRehash<span style="color: #009900;">&#40;</span><span style="color: #000088;">$hashedValue</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php namespace Illuminate\Contracts\Hashing;
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
    }</p></div>
    ;i:2;s:10499:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">namespace</span> Illuminate\Hashing<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">use</span> RuntimeException<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">use</span> Illuminate\Contracts\Hashing\Hasher <span style="color: #b1b100;">as</span> HasherContract<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">class</span> BcryptHasher <span style="color: #000000; font-weight: bold;">implements</span> HasherContract <span style="color: #009900;">&#123;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Default crypt cost factor.
    *
    * @var int
    */</span>
    <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000088;">$rounds</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">10</span><span style="color: #339933;">;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Hash the given value.
    *
    * @param  string  $value
    * @param  array   $options
    * @return string
    *
    * @throws \RuntimeException
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> make<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$cost</span> <span style="color: #339933;">=</span> <span style="color: #990000;">isset</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$options</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'rounds'</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> ? <span style="color: #000088;">$options</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'rounds'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">:</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">rounds</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$hash</span> <span style="color: #339933;">=</span> password_hash<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> PASSWORD_BCRYPT<span style="color: #339933;">,</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'cost'</span> <span style="color: #339933;">=&gt;</span> <span style="color: #000088;">$cost</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$hash</span> <span style="color: #339933;">===</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> RuntimeException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Bcrypt hashing not supported.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #b1b100;">return</span> <span style="color: #000088;">$hash</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Check the given plain value against a hash.
    *
    * @param  string  $value
    * @param  string  $hashedValue
    * @param  array   $options
    * @return bool
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> check<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> <span style="color: #000088;">$hashedValue</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">return</span> password_verify<span style="color: #009900;">&#40;</span><span style="color: #000088;">$value</span><span style="color: #339933;">,</span> <span style="color: #000088;">$hashedValue</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Check if the given hash has been hashed using the given options.
    *
    * @param  string  $hashedValue
    * @param  array   $options
    * @return bool
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> needsRehash<span style="color: #009900;">&#40;</span><span style="color: #000088;">$hashedValue</span><span style="color: #339933;">,</span> <span style="color: #990000;">array</span> <span style="color: #000088;">$options</span> <span style="color: #339933;">=</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$cost</span> <span style="color: #339933;">=</span> <span style="color: #990000;">isset</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$options</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'rounds'</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> ? <span style="color: #000088;">$options</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'rounds'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">:</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">rounds</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">return</span> password_needs_rehash<span style="color: #009900;">&#40;</span><span style="color: #000088;">$hashedValue</span><span style="color: #339933;">,</span> PASSWORD_BCRYPT<span style="color: #339933;">,</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'cost'</span> <span style="color: #339933;">=&gt;</span> <span style="color: #000088;">$cost</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Set the default password work factor.
    *
    * @param  int  $rounds
    * @return $this
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setRounds<span style="color: #009900;">&#40;</span><span style="color: #000088;">$rounds</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">rounds</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>int<span style="color: #009900;">&#41;</span> <span style="color: #000088;">$rounds</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php namespace Illuminate\Hashing;
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
    $cost = isset($options['rounds']) ? $options['rounds'] : $this-&gt;rounds;
    $hash = password_hash($value, PASSWORD_BCRYPT, array('cost' =&gt; $cost));
    if ($hash === false)
    {
    throw new RuntimeException(&quot;Bcrypt hashing not supported.&quot;);
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
    $cost = isset($options['rounds']) ? $options['rounds'] : $this-&gt;rounds;
    return password_needs_rehash($hashedValue, PASSWORD_BCRYPT, array('cost' =&gt; $cost));
    }
    /**
    * Set the default password work factor.
    *
    * @param  int  $rounds
    * @return $this
    */
    public function setRounds($rounds)
    {
    $this-&gt;rounds = (int) $rounds;
    return $this;
    }
    }</p></div>
    ;i:3;s:3692:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">namespace</span> Illuminate\Hashing<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">use</span> Illuminate\Support\ServiceProvider<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">class</span> HashServiceProvider <span style="color: #000000; font-weight: bold;">extends</span> ServiceProvider <span style="color: #009900;">&#123;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Indicates if loading of the provider is deferred.
    *
    * @var bool
    */</span>
    <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000088;">$defer</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Register the service provider.
    *
    * @return void
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> register<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">app</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">singleton</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'hash'</span><span style="color: #339933;">,</span> <span style="color: #000000; font-weight: bold;">function</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #b1b100;">return</span> <span style="color: #000000; font-weight: bold;">new</span> BcryptHasher<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Get the services provided by the provider.
    *
    * @return array
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> provides<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">return</span> <span style="color: #990000;">array</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'hash'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php namespace Illuminate\Hashing;
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
    $this-&gt;app-&gt;singleton('hash', function() { return new BcryptHasher; });
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
    }</p></div>
    ;i:4;s:1525:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">app</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">singleton</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'hash'</span><span style="color: #339933;">,</span> <span style="color: #000000; font-weight: bold;">function</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$app</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #b1b100;">return</span> <span style="color: #000000; font-weight: bold;">new</span> Hasher<span style="color: #009900;">&#40;</span><span style="color: #000088;">$app</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'config'</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'hash'</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">$this-&gt;app-&gt;singleton('hash', function($app) { return new Hasher($app['config']['hash']); });</p></div>
    ;i:5;s:1390:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">app</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">make</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'hash'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">make</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'password'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">app</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">'hash'</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">make</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'password'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">$this-&gt;app-&gt;make('hash')-&gt;make('password');
    $this-&gt;app['hash']-&gt;make('password');</p></div>
    ;i:6;s:1650:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">namespace</span> Illuminate\Support\Facades<span style="color: #339933;">;</span>
    <span style="color: #009933; font-style: italic;">/**
    * @see \Illuminate\Hashing\BcryptHasher
    */</span>
    <span style="color: #000000; font-weight: bold;">class</span> <span style="color: #990000;">Hash</span> <span style="color: #000000; font-weight: bold;">extends</span> Facade <span style="color: #009900;">&#123;</span>
    <span style="color: #009933; font-style: italic;">/**
    * Get the registered name of the component.
    *
    * @return string
    */</span>
    <span style="color: #000000; font-weight: bold;">protected</span> static <span style="color: #000000; font-weight: bold;">function</span> getFacadeAccessor<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">'hash'</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php namespace Illuminate\Support\Facades;
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
    }</p></div>
    ;i:7;s:516:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #990000;">Hash</span><span style="color: #339933;">::</span><span style="color: #004000;">make</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'password'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Hash::make('password');</p></div>
    ";}
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