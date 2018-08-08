# Global Scope

If you do not define your variables locally then they will be available globally within your scripts. This can be very dangerous, can cause difficult to debug bugs so use with care. It can be better to share data between scripts with a Lua module rather than to put data into the global scope for example.

Sometimes you do want to put functions / modules / data into the global scope. It's as easy as not putting local before your definitions. For example, you might want to use the [log module](https://github.com/subsoap/log) and to have it able to be used in all of your scripts without needing to require it in every script. To do so, you would require it once in your main entrypoint. For example, in the main.script of your main.collection.

```lua
log = require("log.log") -- log is global!
```

It's also possible to replace some tables within the global scope at runtime - such as replacing the builtin print function. Know that it's possible but use it with care as you can break the way the engine is meant to work if you're not careful!

If you don't want to mess with the global scope then always remember to add local before every definition you make in your scripts.

