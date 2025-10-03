## Executing Rollback
<br>

The ```kubectl rollout undo``` command lets you go back to the previous version of your app if the new one has problems. Every time you update your app, Kubernetes saves a copy. If something breaks, this command tells Kubernetes to switch back to the last working version.




