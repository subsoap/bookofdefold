---
description: How to create and use Lua modules.
---

# Lua Modules

Lua modules are useful for sharing functions and data between your scripts. 

To be able to share data between scripts make sure you have "shared state" checked in your game.project file.

You can create a Lua module by right clicking on the asset panel and going New -&gt; Lua Module you can then name this file and create it.

This is just a .lua file which can be created with other tools as well.

The default Lua module is blank with some comments only.

The standard pattern for a Lua module file is as follows:

{% code-tabs %}
{% code-tabs-item title="mymodule.lua" %}
```lua
local M = {}

return M
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Then the standard way to include a Lua module in another script as as follows:

```lua
local mymodule = require("mymodule")
```

If you had your mymodule.lua file within a utils folder then your include would be:

```lua
local mymodule = require("utils.mymodule")
```

We will edit our Lua module to add a function and a variable.

{% code-tabs %}
{% code-tabs-item title="mymodule.lua" %}
```lua
local M = {}
M.secret = 777

function M.hello_world()
    print("Hello World Defold!")
end

return M
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Then in a script we can include and use the module's function:

{% code-tabs %}
{% code-tabs-item title="main.script" %}
```lua
local mymodule = require("utils.mymodule")

function init(self)
	print(mymodule.secret)
	mymodule.secret = 25
	print(mymodule.secret)
	mymodule.hello_world()
end

```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
DEBUG:SCRIPT: 777
DEBUG:SCRIPT: 25
DEBUG:SCRIPT: Hello World Defold!
```

{% file src="../../.gitbook/assets/moduleexample.zip" %}

If you look through the source of assets published on the community portal most of them are Lua modules which follow this similar pattern.

If you wish to share your module then you'll want to give it a catchy name, then put it inside of a folder with that name. For example "log/log.lua" see here [https://github.com/subsoap/log](https://github.com/subsoap/log)

Then in the game.project file you would define the "log" folder as a include dir in the library area. See Log's setup for an example of this.

Sharing modules on Github is currently the most popular way of sharing modules. Again, see how others are done and copy them. There are still many resources which have no Defold version so there is still opportunity for you to contribute to the community! When you do publish something make sure you use a license which has as much freedom for its users as possible if you want people to actually use it. If you want to put your work into the public domain like I generally do then you can use the **Creative Commons Zero v1.0 Universal** license.



