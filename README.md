## customize-root-zone

A sample to describe how to customize root zone.
The code below is from `index.html`.

you should 

1. load zone.js
2. create a customized root zone, and set it to window.__zone_symbol__customizeRootZone
3. load zone-patch-customize-root.js

```javascript
<script type="text/javascript" src="./node_modules/zone.js/dist/zone.js"></script>
  <script type="text/javascript">
    var mySpec = {
      name: "GMAPS",
      onScheduleTask: (delegate, current, target, task) => {
        console.log('schedule task', task.source, Zone.current.name);
        return delegate.scheduleTask(target, task);
      },
      onHasTask: (delegate, current, target, taskState) => {
        console.log('hasTask: ', taskState);
        return delegate.hasTask(target, taskState);
      }
    };
    var mapZone = Zone.current.fork(mySpec);
    window.__zone_symbol__customizeRootZone = mapZone;
  </script>
  <script type="text/javascript" src="./node_modules/zone.js/dist/zone-patch-customize-root.js"></script>
```
