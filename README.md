# iaam-client
## Installation
Before the installation make sure that Java 8 is installed on your OS. Please check it with
```
# java -version
```

### oxd-server Installation
Follow this docs [oxd-server docs](https://gluu.org/docs/oxd/3.1.4/install/).


### Prerequisites
- Node >= 6.x.x and NPM >= 3.x.x
- npm 3.10.10


### Install dependencies 

```
npm i
```       

### Install API Secur
Download [API Secur](https://github.com/jponharn/api-secur).

## Configuration
copy setting.json.tmp to setting.json and then config them file.

Application starting at port: "client_port"
```
{
    "op_host": "https://iaamdemo.lsr.nectec.or.th",
    "client_port": "8001",
    "client_name": "",
    "api_endpoint": "",
    "oxd_setting": {
        "https_extension": false,
        "host": "localhost",
        "port": 8099
    },
    "oxd_id": "",
    "reg": {
    }
}
```    

## Run
```
node serve.js
```

# Register Site
```
oxd.register_site({
        op_host: "https://iaamdemo.lsr.nectec.or.th",
        authorization_redirect_uri: "https://localhost:8001/callback",
        post_logout_redirect_uri: "https://localhost:8001/callback",
        scope: ["openid", "email", "profile", "uma_protection"],
        grant_types: ["authorization_code", "client_credentials"],
        client_name: "client name"
      }, (err, response) => {
        if (err) {
          console.log('Error : ', err);
          res.send(err)
        }
        setting.oxd_id = response.data.oxd_id
        res.status(200).send({'status':'OK'})
      });
```
**Response:**
```
{
    "status":"ok",
    "data":{
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF"
    }
}
```

# Remove Site
```
oxd.remove_site({
        oxd_id: "<oxd_id>"
    }, (err, response) => {
        if (err) {
            console.log('Error : ', err)
            res.send(err)
        }
        if(response.status == 'ok'){
            setting.reg = {}
            setting.oxd_id = ""
        }
        res.status(200).send(response)
    });
```
**Response:**
```
{
    "status":"ok",
    "data": {
        "oxd_id": "6F9619FF-8B86-D011-B42D-00CF4FC964FF"
    }
}
```