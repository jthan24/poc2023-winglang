# Installation
```bash
npm install -g winglang
wing --version
wing docs
```

## VS Code plugin
This tool have a plugin on VSCode for made more easy writing code task

# Hello Wing
```bash
mkdir hello-wing && cd hello-wing && touch main.w
```
## Our fist file
This code should be mostly self explanatory. We define a queue and a counter, and every time a message is added to the queue, a handler is triggered and creates a file named wing-<counter-index>.txt with "Hello, ${message}!" content, and the counter is incremented by 1.

```js
bring cloud;

let bucket = new cloud.Bucket();
let counter = new cloud.Counter(initial: 1);
let queue = new cloud.Queue();

queue.setConsumer(inflight (message: str) => {
  let index = counter.inc();
    bucket.put("wing-${index}.txt", "Hello, ${message}");
	  log("file wing-${index}.txt created");
	  });
```
## Run locally
```bash
wing it main.w
```

## Deploy to AWS
```bash
# Compile to create a terraform output
wing compile --target tf-aws main.w
cd ./target/main.tfaws
terraform init
terraform plan
terraform apply
terraform destroy
```


## Deploy to Azure - beta
```bash
AZURE_LOCATION=eastus2 wing compile --target tf-azure main.w
```

## Deploy to GCP - beta
```bash
GOOGLE_PROJECT_ID=123sdfs GOOGLE_STORAGE_LOCATION=NORTHAMERICA-NORTHEAST2 wing compile --target tf-gcp main.w
```


# References
https://github.com/winglang/examples/blob/main/examples/hello-wing/main.w
https://www.winglang.io/docs/standard-library/util/api-reference
https://github.com/winglang/wing/issues?q=is%3Aissue+is%3Aopen+tag
