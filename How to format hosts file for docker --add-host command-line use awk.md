## 单值
`$(cat ~/yapi_env_hosts|awk -F '[# \r\n]*' '($1 && $1 !~ /^[#]*$/){printf "--add-host="$2":"$1" "}')`
https://awk.js.org/?gist=c931882a5022c5a5ae7d15459bd2aa6d

## 多值
`$(cat ~/yapi_env_hosts|awk '{for(i=1;i<=NF;i++){ arr[i]=$i}}{for(i=2;i<=NF;i++){ if($1!~/^#/) { print "--add-host="arr[i]":"$1" "}}}')`
https://awk.js.org/?gist=0c576ecc0ec3d17993204a739baa2a28


## Example

```javascript
exec(`
  docker run --rm \
  --name runner_1 \
  -p 3000:3000 \
  -p 27017 \
  $(cat ~/yapi_env_hosts|awk -F '[# \r\n]*' '($1 && $1 !~ /^[#]*$/){printf "--add-host="$2":"$1" "}') \
  node:latest \
  ${process.argv[2] === 'dev' && "node ./server/app.js dev"}
`)
```
