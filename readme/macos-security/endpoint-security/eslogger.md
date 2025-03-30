---
icon: left-to-bracket
---

# eslogger

## The _eslogger_ Tool

With the release of the Endpoint Security Framework (ESF) in macOS 10.15 (2019), Apple introduced an API for monitoring and auditing system events to replace the deprecated [OpenBSM](https://en.wikipedia.org/wiki/OpenBSM) API. Security products now ingest these system events via the macOS agent. However, accessing these raw ESF events in an ad-hoc manner required either self-developed software notarized by Apple or a third-party ESF client like esf-playground from [mittenmac](https://themittenmac.com/the-esf-playground/).&#x20;

The October 2022 release of macOS 13.0, named Ventura, includes _eslogger_: _“eslogger interfaces with Endpoint Security to log events to standard output or to the unified logging system.”_&#x20;

## Setup and Test Run&#x20;

For the first eslogger test, we set up our system to examine events that the system creates while performing standard operations, such as opening folders and reading files.

Before eslogger can function, the app that executes eslogger must have full disk access. We granted this access to the Terminal app:\


<figure><img src="https://www.cybereason.com/hs-fs/hubfs/image7-Oct-03-2022-04-45-09-68-PM.png?width=588&#x26;name=image7-Oct-03-2022-04-45-09-68-PM.png" alt=""><figcaption></figcaption></figure>

At the time of writing this post, eslogger supports 82 different endpoint security events, including several undocumented ones.. All supported events can be listed via:

```
% sudo eslogger --list-events
```



***

## REFERENCES

* [https://developer.apple.com/documentation/endpointsecurity/event\_types](https://developer.apple.com/documentation/endpointsecurity/event_types)
* [https://www.cybereason.com/blog/blue-teaming-on-macos-with-eslogger](https://www.cybereason.com/blog/blue-teaming-on-macos-with-eslogger)
* [https://www.youtube.com/watch?v=3D\_qsdVRYS0\&ab\_channel=AppleDeveloper](https://www.youtube.com/watch?v=3D_qsdVRYS0\&ab_channel=AppleDeveloper)

