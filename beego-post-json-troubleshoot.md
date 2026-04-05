By default, Beego v2 does not store the request body in memory for performance reasons. Accessing **c.Ctx.Input.RequestBody** will return empty bytes unless configured.
## Solution:
In conf/app.conf, add:
```bash
copyrequestbody = true
```
Restart Beego after editing:
```bash
bee run
```
