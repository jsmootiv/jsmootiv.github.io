---
layout: post
title: Disable cashaddress on BCH node
excerpt: "Here is how you disable the"
permalink: /disable-cashaddress-on-BCH-node/
tags:
  - bitcoin cash
  - blockchain
---
Here is a quick little note for those who may be upgrading [Bitcoin ABC to 0.17 for the hard fork](https://www.bitcoinabc.org/).

About a week ago we built a container to comply with the Bitcoin Cash hardfork but there was an issue deploying.

All of the addresses returned by the node are in the new [Bitcoin Cash address format](https://github.com/bitcoincashorg/bitcoincash.org/blob/master/spec/cashaddr.md).

I shot an email to the Bitcoin ABC team and thankfully they are very responsive. They let me know that if you add a setting `usecashaddr=0` the node will revert to using the old address format.

This flag isn't really documented so I'm adding it here to hopefully save some other folks from having issues.