# [post.w](../../../../../../examples/tests/sdk_tests/api/post.w) | compile | tf-aws

## inflight.$Closure1.js
```js
module.exports = function({ api_POST, body, std_Json }) {
  class $Closure1 {
    constructor({  }) {
      const $obj = (...args) => this.handle(...args);
      Object.setPrototypeOf($obj, this);
      return $obj;
    }
    async $inflight_init()  {
    }
    async handle(req)  {
      {((cond) => {if (!cond) throw new Error("assertion failed: req.method == api_POST")})((req.method === api_POST))};
      {((cond) => {if (!cond) throw new Error("assertion failed: req.path == \"/path\"")})((req.path === "/path"))};
      {((cond) => {if (!cond) throw new Error("assertion failed: req.body == Json.stringify(body)")})((req.body === ((args) => { return JSON.stringify(args[0], null, args[1]) })([body])))};
      {((cond) => {if (!cond) throw new Error("assertion failed: req.headers?.get(\"content-type\") == \"application/json\"")})(((req.headers)["content-type"] === "application/json"))};
      return {
      "status": 200,
      "body": req.body,}
      ;
    }
  }
  return $Closure1;
}

```

## inflight.$Closure2.js
```js
module.exports = function({ api, body, http_POST, http_Util, std_Json }) {
  class $Closure2 {
    constructor({  }) {
      const $obj = (...args) => this.handle(...args);
      Object.setPrototypeOf($obj, this);
      return $obj;
    }
    async $inflight_init()  {
    }
    async handle()  {
      const url = (api.url + "/path");
      const response = (await http_Util.post(url,{
      "headers": Object.freeze({"content-type":"application/json"}),
      "body": ((args) => { return JSON.stringify(args[0], null, args[1]) })([body]),}
      ));
      const fetchResponse = (await http_Util.post(url,{
      "method": http_POST,
      "headers": Object.freeze({"content-type":"application/json"}),
      "body": ((args) => { return JSON.stringify(args[0], null, args[1]) })([body]),}
      ));
      {((cond) => {if (!cond) throw new Error("assertion failed: response.body == Json.stringify(body)")})((response.body === ((args) => { return JSON.stringify(args[0], null, args[1]) })([body])))};
      {((cond) => {if (!cond) throw new Error("assertion failed: response.status == 200")})((response.status === 200))};
      {((cond) => {if (!cond) throw new Error("assertion failed: response.url == url")})((response.url === url))};
      {((cond) => {if (!cond) throw new Error("assertion failed: fetchResponse.body == Json.stringify(body)")})((fetchResponse.body === ((args) => { return JSON.stringify(args[0], null, args[1]) })([body])))};
      {((cond) => {if (!cond) throw new Error("assertion failed: fetchResponse.status == 200")})((fetchResponse.status === 200))};
      {((cond) => {if (!cond) throw new Error("assertion failed: fetchResponse.url == url")})((fetchResponse.url === url))};
    }
  }
  return $Closure2;
}

```

## main.tf.json
```json
{
  "//": {
    "metadata": {
      "backend": "local",
      "stackName": "root",
      "version": "0.17.0"
    },
    "outputs": {
      "root": {
        "Default": {
          "cloud.TestRunner": {
            "TestFunctionArns": "WING_TEST_RUNNER_FUNCTION_ARNS"
          }
        }
      }
    }
  },
  "data": {
    "aws_region": {
      "Region": {
        "//": {
          "metadata": {
            "path": "root/Default/Region",
            "uniqueId": "Region"
          }
        }
      }
    }
  },
  "output": {
    "WING_TEST_RUNNER_FUNCTION_ARNS": {
      "value": "[[\"root/Default/Default/test:http.post and http.fetch can preform a call to an api\",\"${aws_lambda_function.testhttppostandhttpfetchcanpreformacalltoanapi_Handler_C4853DBD.arn}\"]]"
    }
  },
  "provider": {
    "aws": [
      {}
    ]
  },
  "resource": {
    "aws_api_gateway_deployment": {
      "cloudApi_api_deployment_545514BF": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/api/deployment",
            "uniqueId": "cloudApi_api_deployment_545514BF"
          }
        },
        "lifecycle": {
          "create_before_destroy": true
        },
        "rest_api_id": "${aws_api_gateway_rest_api.cloudApi_api_2B334D75.id}",
        "triggers": {
          "redeployment": "2e0d4578fa0f01cc502b493b801d616ab05c6da5"
        }
      }
    },
    "aws_api_gateway_rest_api": {
      "cloudApi_api_2B334D75": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/api/api",
            "uniqueId": "cloudApi_api_2B334D75"
          }
        },
        "body": "{\"openapi\":\"3.0.3\",\"paths\":{\"/path\":{\"post\":{\"operationId\":\"post-path\",\"responses\":{\"200\":{\"description\":\"200 response\",\"content\":{}}},\"parameters\":[],\"x-amazon-apigateway-integration\":{\"uri\":\"arn:aws:apigateway:${data.aws_region.Region.name}:lambda:path/2015-03-31/functions/${aws_lambda_function.cloudApi_cloudApi-OnRequest-cdafee6e_A6C8366F.arn}/invocations\",\"type\":\"aws_proxy\",\"httpMethod\":\"POST\",\"responses\":{\"default\":{\"statusCode\":\"200\"}},\"passthroughBehavior\":\"when_no_match\",\"contentHandling\":\"CONVERT_TO_TEXT\"}}}}}",
        "name": "api-c895068c"
      }
    },
    "aws_api_gateway_stage": {
      "cloudApi_api_stage_BBB283E4": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/api/stage",
            "uniqueId": "cloudApi_api_stage_BBB283E4"
          }
        },
        "deployment_id": "${aws_api_gateway_deployment.cloudApi_api_deployment_545514BF.id}",
        "rest_api_id": "${aws_api_gateway_rest_api.cloudApi_api_2B334D75.id}",
        "stage_name": "prod"
      }
    },
    "aws_iam_role": {
      "cloudApi_cloudApi-OnRequest-cdafee6e_IamRole_4382C442": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/cloud.Api-OnRequest-cdafee6e/IamRole",
            "uniqueId": "cloudApi_cloudApi-OnRequest-cdafee6e_IamRole_4382C442"
          }
        },
        "assume_role_policy": "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Action\":\"sts:AssumeRole\",\"Principal\":{\"Service\":\"lambda.amazonaws.com\"},\"Effect\":\"Allow\"}]}"
      },
      "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRole_364748FC": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/test:http.post and http.fetch can preform a call to an api/Handler/IamRole",
            "uniqueId": "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRole_364748FC"
          }
        },
        "assume_role_policy": "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Action\":\"sts:AssumeRole\",\"Principal\":{\"Service\":\"lambda.amazonaws.com\"},\"Effect\":\"Allow\"}]}"
      }
    },
    "aws_iam_role_policy": {
      "cloudApi_cloudApi-OnRequest-cdafee6e_IamRolePolicy_8BF9C89F": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/cloud.Api-OnRequest-cdafee6e/IamRolePolicy",
            "uniqueId": "cloudApi_cloudApi-OnRequest-cdafee6e_IamRolePolicy_8BF9C89F"
          }
        },
        "policy": "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Effect\":\"Allow\",\"Action\":\"none:null\",\"Resource\":\"*\"}]}",
        "role": "${aws_iam_role.cloudApi_cloudApi-OnRequest-cdafee6e_IamRole_4382C442.name}"
      },
      "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRolePolicy_720C559E": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/test:http.post and http.fetch can preform a call to an api/Handler/IamRolePolicy",
            "uniqueId": "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRolePolicy_720C559E"
          }
        },
        "policy": "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Effect\":\"Allow\",\"Action\":\"none:null\",\"Resource\":\"*\"}]}",
        "role": "${aws_iam_role.testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRole_364748FC.name}"
      }
    },
    "aws_iam_role_policy_attachment": {
      "cloudApi_cloudApi-OnRequest-cdafee6e_IamRolePolicyAttachment_5383D6A2": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/cloud.Api-OnRequest-cdafee6e/IamRolePolicyAttachment",
            "uniqueId": "cloudApi_cloudApi-OnRequest-cdafee6e_IamRolePolicyAttachment_5383D6A2"
          }
        },
        "policy_arn": "arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole",
        "role": "${aws_iam_role.cloudApi_cloudApi-OnRequest-cdafee6e_IamRole_4382C442.name}"
      },
      "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRolePolicyAttachment_E623498E": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/test:http.post and http.fetch can preform a call to an api/Handler/IamRolePolicyAttachment",
            "uniqueId": "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRolePolicyAttachment_E623498E"
          }
        },
        "policy_arn": "arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole",
        "role": "${aws_iam_role.testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRole_364748FC.name}"
      }
    },
    "aws_lambda_function": {
      "cloudApi_cloudApi-OnRequest-cdafee6e_A6C8366F": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/cloud.Api-OnRequest-cdafee6e/Default",
            "uniqueId": "cloudApi_cloudApi-OnRequest-cdafee6e_A6C8366F"
          }
        },
        "environment": {
          "variables": {
            "WING_FUNCTION_NAME": "cloud-Api-OnRequest-cdafee6e-c8147384",
            "WING_TARGET": "tf-aws"
          }
        },
        "function_name": "cloud-Api-OnRequest-cdafee6e-c8147384",
        "handler": "index.handler",
        "publish": true,
        "role": "${aws_iam_role.cloudApi_cloudApi-OnRequest-cdafee6e_IamRole_4382C442.arn}",
        "runtime": "nodejs18.x",
        "s3_bucket": "${aws_s3_bucket.Code.bucket}",
        "s3_key": "${aws_s3_object.cloudApi_cloudApi-OnRequest-cdafee6e_S3Object_5DAAA0EF.key}",
        "timeout": 30,
        "vpc_config": {
          "security_group_ids": [],
          "subnet_ids": []
        }
      },
      "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_C4853DBD": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/test:http.post and http.fetch can preform a call to an api/Handler/Default",
            "uniqueId": "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_C4853DBD"
          }
        },
        "environment": {
          "variables": {
            "CLOUD_API_C82DF3A5": "${aws_api_gateway_stage.cloudApi_api_stage_BBB283E4.invoke_url}",
            "WING_FUNCTION_NAME": "Handler-c88947b5",
            "WING_TARGET": "tf-aws",
            "WING_TOKEN_TFTOKEN_TOKEN_21": "${jsonencode(aws_api_gateway_stage.cloudApi_api_stage_BBB283E4.invoke_url)}"
          }
        },
        "function_name": "Handler-c88947b5",
        "handler": "index.handler",
        "publish": true,
        "role": "${aws_iam_role.testhttppostandhttpfetchcanpreformacalltoanapi_Handler_IamRole_364748FC.arn}",
        "runtime": "nodejs18.x",
        "s3_bucket": "${aws_s3_bucket.Code.bucket}",
        "s3_key": "${aws_s3_object.testhttppostandhttpfetchcanpreformacalltoanapi_Handler_S3Object_BEC67279.key}",
        "timeout": 30,
        "vpc_config": {
          "security_group_ids": [],
          "subnet_ids": []
        }
      }
    },
    "aws_lambda_permission": {
      "cloudApi_api_permission-POST-e2131352_099525EE": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/api/permission-POST-e2131352",
            "uniqueId": "cloudApi_api_permission-POST-e2131352_099525EE"
          }
        },
        "action": "lambda:InvokeFunction",
        "function_name": "${aws_lambda_function.cloudApi_cloudApi-OnRequest-cdafee6e_A6C8366F.function_name}",
        "principal": "apigateway.amazonaws.com",
        "source_arn": "${aws_api_gateway_rest_api.cloudApi_api_2B334D75.execution_arn}/*/POST/path",
        "statement_id": "AllowExecutionFromAPIGateway-POST-e2131352"
      }
    },
    "aws_s3_bucket": {
      "Code": {
        "//": {
          "metadata": {
            "path": "root/Default/Code",
            "uniqueId": "Code"
          }
        },
        "bucket_prefix": "code-c84a50b1-"
      }
    },
    "aws_s3_object": {
      "cloudApi_cloudApi-OnRequest-cdafee6e_S3Object_5DAAA0EF": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/cloud.Api/cloud.Api-OnRequest-cdafee6e/S3Object",
            "uniqueId": "cloudApi_cloudApi-OnRequest-cdafee6e_S3Object_5DAAA0EF"
          }
        },
        "bucket": "${aws_s3_bucket.Code.bucket}",
        "key": "<ASSET_KEY>",
        "source": "<ASSET_SOURCE>"
      },
      "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_S3Object_BEC67279": {
        "//": {
          "metadata": {
            "path": "root/Default/Default/test:http.post and http.fetch can preform a call to an api/Handler/S3Object",
            "uniqueId": "testhttppostandhttpfetchcanpreformacalltoanapi_Handler_S3Object_BEC67279"
          }
        },
        "bucket": "${aws_s3_bucket.Code.bucket}",
        "key": "<ASSET_KEY>",
        "source": "<ASSET_SOURCE>"
      }
    }
  }
}
```

## preflight.js
```js
const $stdlib = require('@winglang/sdk');
const $outdir = process.env.WING_SYNTH_DIR ?? ".";
const std = $stdlib.std;
const $wing_is_test = process.env.WING_IS_TEST === "true";
const $AppBase = $stdlib.core.App.for(process.env.WING_TARGET);
const cloud = require('@winglang/sdk').cloud;
const http = require('@winglang/sdk').http;
class $Root extends $stdlib.std.Resource {
  constructor(scope, id) {
    super(scope, id);
    class $Closure1 extends $stdlib.std.Resource {
      constructor(scope, id, ) {
        super(scope, id);
        this.display.hidden = true;
        this._addInflightOps("handle");
      }
      static _toInflightType(context) {
        const self_client_path = "././inflight.$Closure1.js";
        const api_POST_client = context._lift(api_POST);
        const body_client = context._lift(body);
        const std_JsonClient = std.Json._toInflightType(context);
        return $stdlib.core.NodeJsCode.fromInline(`
          require("${self_client_path}")({
            api_POST: ${api_POST_client},
            body: ${body_client},
            std_Json: ${std_JsonClient.text},
          })
        `);
      }
      _toInflight() {
        return $stdlib.core.NodeJsCode.fromInline(`
          (await (async () => {
            const $Closure1Client = ${$Closure1._toInflightType(this).text};
            const client = new $Closure1Client({
            });
            if (client.$inflight_init) { await client.$inflight_init(); }
            return client;
          })())
        `);
      }
      _registerBind(host, ops) {
        if (ops.includes("$inflight_init")) {
          $Closure1._registerBindObject(api_POST, host, []);
          $Closure1._registerBindObject(body, host, []);
        }
        if (ops.includes("handle")) {
          $Closure1._registerBindObject(api_POST, host, []);
          $Closure1._registerBindObject(body, host, []);
        }
        super._registerBind(host, ops);
      }
    }
    class $Closure2 extends $stdlib.std.Resource {
      constructor(scope, id, ) {
        super(scope, id);
        this.display.hidden = true;
        this._addInflightOps("handle");
      }
      static _toInflightType(context) {
        const self_client_path = "././inflight.$Closure2.js";
        const api_client = context._lift(api);
        const body_client = context._lift(body);
        const http_POST_client = context._lift(http_POST);
        const http_UtilClient = http.Util._toInflightType(context);
        const std_JsonClient = std.Json._toInflightType(context);
        return $stdlib.core.NodeJsCode.fromInline(`
          require("${self_client_path}")({
            api: ${api_client},
            body: ${body_client},
            http_POST: ${http_POST_client},
            http_Util: ${http_UtilClient.text},
            std_Json: ${std_JsonClient.text},
          })
        `);
      }
      _toInflight() {
        return $stdlib.core.NodeJsCode.fromInline(`
          (await (async () => {
            const $Closure2Client = ${$Closure2._toInflightType(this).text};
            const client = new $Closure2Client({
            });
            if (client.$inflight_init) { await client.$inflight_init(); }
            return client;
          })())
        `);
      }
      _registerBind(host, ops) {
        if (ops.includes("$inflight_init")) {
          $Closure2._registerBindObject(api, host, []);
          $Closure2._registerBindObject(body, host, []);
          $Closure2._registerBindObject(http_POST, host, []);
        }
        if (ops.includes("handle")) {
          $Closure2._registerBindObject(api.url, host, []);
          $Closure2._registerBindObject(body, host, []);
          $Closure2._registerBindObject(http_POST, host, []);
        }
        super._registerBind(host, ops);
      }
    }
    const http_POST = http.HttpMethod.POST;
    const api_POST = cloud.HttpMethod.POST;
    const api = this.node.root.newAbstract("@winglang/sdk.cloud.Api",this,"cloud.Api");
    const body = Object.freeze({"cat":"Tion"});
    (api.post("/path",new $Closure1(this,"$Closure1")));
    this.node.root.new("@winglang/sdk.std.Test",std.Test,this,"test:http.post and http.fetch can preform a call to an api",new $Closure2(this,"$Closure2"));
  }
}
class $App extends $AppBase {
  constructor() {
    super({ outdir: $outdir, name: "post", plugins: $plugins, isTestEnvironment: $wing_is_test });
    if ($wing_is_test) {
      new $Root(this, "env0");
      const $test_runner = this.testRunner;
      const $tests = $test_runner.findTests();
      for (let $i = 1; $i < $tests.length; $i++) {
        new $Root(this, "env" + $i);
      }
    } else {
      new $Root(this, "Default");
    }
  }
}
new $App().synth();

```
