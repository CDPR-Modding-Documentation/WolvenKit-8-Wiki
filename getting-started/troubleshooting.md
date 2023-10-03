---
description: What to do when your Wolvenkit install acts up
---

# Troubleshooting

{% hint style="info" %}
This is the troubleshooting page for your **Wolvenkit install**.&#x20;

For game issues, check [Troubleshooting](http://127.0.0.1:5000/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/user-guide-troubleshooting "mention")on [Cyberpunk 2077 Modding](http://127.0.0.1:5000/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention").

For issues with **modding workflows**, refer to the corresponding section of the guides or use the search function of [Cyberpunk 2077 Modding](http://127.0.0.1:5000/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention").
{% endhint %}

## Basic Troubleshooting steps

### .NET

The different libraries in Wolvenkit require both [.NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) and [.NET 7.0](https://dotnet.microsoft.com/en-us/download/dotnet/7.0). Make sure to install both!

### Clean reinstall

Remove everything inside your Wolvenkit install folder, then download the latest release from github and extract the files into your empty directory.&#x20;

If that doesn't solve the problem:

### %Appdata%

You can find Wolvenkit's settings (including your project layout) in the following folder:

```
%appdata%\REDModding\WolvenKit
```

Maybe something here will help you resolve that error.

### Get in touch

If these (admittedly basic) steps didn't help you resolve the issue, you can get in touch on the [REDmodding discord](https://discord.gg/redmodding) in the `#wolvenkit-support` channel.
