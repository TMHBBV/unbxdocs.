---
title: 'Initialize SDK '
deprecated: false
hidden: false
metadata:
  robots: index
---
To initialize SDK, import Unbxd framework:import com.unbxd.sdk.Client

Unbxd is initialised with API key and Site key:

```Text Kotlin
val client = Client(,, *applicationContext*) 
```
```Text Java
Client client= new Client(SITE_ID, API_KEY, context.getApplicationContext());
```

> 📘 NOTE
>
> We advise you to use your API Key in encrypted form on your frontend and never share it with anyone.