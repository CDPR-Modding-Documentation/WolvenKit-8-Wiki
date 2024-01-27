---
description: What to do when your Wolvenkit install acts up
---

# Troubleshooting

{% hint style="info" %}
This is the troubleshooting page for your **Wolvenkit install**.&#x20;

For game issues, check [Troubleshooting](https://app.gitbook.com/s/4gzcGtLrr90pVjAWVdTc/for-mod-users/user-guide-troubleshooting "mention")on [Cyberpunk 2077 Modding](https://app.gitbook.com/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention").

For issues with **modding workflows**, refer to the corresponding section of the guides or use the search function of [Cyberpunk 2077 Modding](https://app.gitbook.com/o/-MP5ijqI11FeeX7c8-N8/s/4gzcGtLrr90pVjAWVdTc/ "mention").
{% endhint %}

{% hint style="success" %}
If you've run into a problem that isn't on this list, please **reach out**!

* If you have solved the problem already, feel free to [edit the wiki](https://app.gitbook.com/invite/-MP5ijqI11FeeX7c8-N8/H70HZBOeUulIpkQnBLK7)!

Otherwise, you can either find us on [Discord](https://discord.gg/redmodding) (`#wolvenkit-support`), or, if you know that it's a technical issue, [file an issue on github](https://github.com/WolvenKit/Wolvenkit/issues) or open a thread on Discord's `#wkit-bugs-and-requests` channel.
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
