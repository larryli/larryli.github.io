---
ID: 262638
post_title: Why the GUI of ReactOS is so slow…
author: 南 靖男
post_date: 2005-02-20 16:33:30
post_excerpt: ""
layout: post
permalink: 2005/02/262638
published: true
---
<a href="http://blogs.reactos.com/w3seek/archive/2005/01/20/164.aspx">http://blogs.reactos.com/w3seek/archive/2005/01/20/164.aspx</a>

<!--more-->I've seen people asking this question over and over again, here's why:
Excessive locks of objects influence scheduling badly, in other words each time you just attempt to move the mouse e.g. the user handle table (which stores handles for windows, cursors, hot keys...) is accessed several hundreds of times. But why? Well, there's lots of things that need to be done one e.g. a single mouse move: Actually move the mouse (which itself is pretty fast), then the window below the cursor needs to be notified. This is Where&nbsp;it gets ugly. The list of all windows on the desktop needs to be enumerated - each time a window object gets locked. Then it needs to be determined whether the cursor is in the window, if so a (few) message(s) will be sent, which cause the handle to be locked yet another time. And not just the handle, also the message queue of the corresponding thread. And this is only a very much simplified example of what happens on each mouse move (when you move the mouse quickly, you'll see the CPU time go up to 100%!).
It's even a lot more complicated when doing e.g. window repaints, move/resize of windows, .... All sorts of things just lock handles all over again. It works with minimum losings when only one thread is involved in the locking mechanisms, but the more stable ReactOS becomes, the more threads are running (applications) simultaneously and do various tasks which you might not be aware of because not everything actually means doing visual stuff. When you start up or resize e.g. Abiword there are probably a hundred thousand locks on user objects (remember, user objects are just part of the win32 subsystem, I'm not even talking about kernel objects or GDI objects!), each time scheduling is affected, now how on earth would this be fast?!
[b]The reason[/b] for the excessive locks of all sorts of stuff was a bad decision which we (probably mostly me) introduced in the beginnings of the GUI development. So, you can blame me for why ReactOS is so god damn slow, but I've been working on this issue and because ReactOS has become so large it's a bit difficult to actually complete this task alone. Plus, I don't have much time at the moment but I hope I can continue development on this issue some time in February.
[b]The solution[/b] is simply instead of locking stuff all over the place we just use a global shared+exclusive lock. Also instead of using handles inside the subsystem (which is a very bad thing) I'm going to replace them with direct object pointers, which will save unneccessary translations of handles to pointers.
<font color="#0000ff">To avoid misunderstandings: It's neither GDI's (part of win32k which is the actualy graphics subsystem) fault nor the kernel's fault (ntoskrnl), the culprit is the user subsystem (part of win32k which provides stuff like messaging and windowing)!</font>
posted on Thursday, January 20, 2005 1:54 PM