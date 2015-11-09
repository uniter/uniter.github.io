# How to deploy

In order to publish the new docs, we use [Couscous](https://github.com/CouscousPHP/Couscous). It is super simple and efficient.

```
# Install
composer global require couscous/couscous

# Preview. Make sure it's in $PATH
couscous preview

# Deploy!
couscous deploy --branch=master
```

And that's it. :) Happy writing!

BTW, anything within the `misc/` folder is ignored by Couscous.
