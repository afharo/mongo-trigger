# Mongo Stream

Listening to MongoDB live changes using [mongo-oplog](https://github.com/cayasso/mongo-oplog).

This is intended to replace deprecated [mongo-watch](https://github.com/TorchlightSoftware/mongo-watch) and increase its features.

## Install

```bash
npm install mongo-trigger
```

## Usage

Watching a collection is as easy as:

```javascript
var MongoStream = require('mongo-trigger');

var watcher = new MongoStream({format: 'pretty'});

// watch the collection
watcher.watch('test.users', function(event) {
  // parse the results
  console.log('something changed:', event);
}
```

## Options

See the applyDefaults function in [lib/index.js](https://github.com/afharo/mongo-trigger/blob/master/lib/index.js) for a list of options and their defaults.

## Authentication

Pass the "username" and "password" options (and authDB in case it is different to 'admin')

```javascript
var watcher = new MongoStream({username: 'bobross', password: 'happytrees', authdb:'admin'});
```

## Replica sets

If you pass a replicaSet array it will be used to establish a connection.
It should keep working in case the primary changes - i.e. when it dies, and secondary takes it place.

```javascript
var watcher = new MongoStream({
    replicaSet: [
        {host: "currentPrimary.mongoexample.com", port : 10453},
        {host: "currentSecondary.mongoexample.com", port : 10452}
    ]
});
```

## MongoS

I am currently working on supporting connections to MongoS. In this case, this driver will obtain all replicaSets forming the cluster and watch to each shard. This feature will be available in future versions (any help will be very welcome).


## Credits

[TorchlightSoftware](https://github.com/TorchlightSoftware) inspired this project with its mongo-watch module.
This couldn't be possible without [cayasso](https://github.com/cayasso)'s mongo-oplog module.

## Contributing

Pull requests welcome!  Please create a feature branch instead of submitting directly to master.  This will help me test/verify before merging.
