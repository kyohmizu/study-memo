- set labels to nodes

```bash
$ kubectl label [nodeName] [key]=[value]
```

- create yaml template

```bash
$ kubectl run [NAME] --image=[IMAGE] --dry-run -o yaml
```

|kind|option|
|--|--|
|deployment|nothing|
|pod|--restart=Never|
|job|--restart=OnFailure|
|cronjob|--schedule='cron format(e.g. 0/5 * * * ?)'|

