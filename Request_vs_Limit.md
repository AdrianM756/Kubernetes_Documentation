## Request vs Limit

| **Term**   | **What It Means**                                           |
|------------|-------------------------------------------------------------|
| Request    | The minimum amount of CPU/memory your app needs.           |
| Limit      | The maximum amount of CPU/memory your app can use.         |
<br>

*Importance:*

* ```Requests``` help Kubernetes decide where to put your app.
* ```Limits``` stop your app from hogging resources and crashing the system.
<br>

*Simplified Analogy:*

```Request``` = “I need at least 8 glasses of water per day.”

```Limit``` = “Do'nt give me more than 8 glasses of water per day or I'll be bloated.”
<br>



