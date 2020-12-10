`$(cat ~/yapi_env_hosts|awk -F '[# \r\n]*' '($1 && $1 !~ /^[#]*$/){printf "--add-host="$2":"$1" "}')`

https://awk.js.org/?gist=c931882a5022c5a5ae7d15459bd2aa6d

## Example

```javascript
exec(`
  docker run --rm \
  --name ${uuName} \
  -p ${currRunner.port}:3000 \
  -p 27017 \
  $(cat ~/yapi_env_hosts|awk -F '[# \r\n]*' '($1 && $1 !~ /^[#]*$/){printf "--add-host="$2":"$1" "}') \
  mfex/yapi:latest \
  ${process.argv[2] === 'dev' && "node ./server/app.js dev"}
`)
```
