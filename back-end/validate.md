validate function refer to joi

value以object传入，其他均用args变参设置，如果最后一个是callback则最后执行

```js
root.validate = function (value, ...args /*, [schema], [options], callback */) {

        const last = args[args.length - 1];
        const callback = typeof last === 'function' ? last : null;

        const count = args.length - (callback ? 1 : 0);
        if (count === 0) {
            return any.validate(value, callback);
        }

        const options = count === 2 ? args[1] : {};
        const schema = root.compile(args[0]);

        return schema._validateWithOptions(value, options, callback);
    };
```

https://github.com/hapijs/joi/blob/v13.1.1/lib/index.js

