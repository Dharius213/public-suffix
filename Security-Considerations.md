### The Public Suffix List Adheres to ICP-3 and IAB Guidance ###
The project does not accept requests for TLD additions that are not part of the one-root ICP-3 concept.

The PSL adheres to the [ICP-3](https://www.icann.org/resources/pages/unique-authoritative-root-2012-02-25-en) "A Unique, Authoritative Root for the DNS".

There are exceptions to strict adherence to the ICP-3, but those are standards-driven or tied to authoritative policies that work within the ICP-3.

Some examples are the .onion TLD, 2012 round nTLDs that were approved TLD applications that have been furnished by ICANN on their contracted TLDs json file, and names defined by RFC(s) that are produced by the Internet Architecture Board (IAB) or Internet Engineering Task Force (IETF).

The project does not create new domain names, but rather documents existing names as defined by the IANA, ICANN, IETF or IAB, and then adds elegance and specificity within that universe without going beyond it.

### ICANN Security and Stability Advisory Committee (SSAC)
ICANN has a [Security and Stability Advisory Committee](https://www.icann.org/resources/pages/ssac-role-2018-02-06-en), with the role of advising the ICANN community and Board on matters relating to the security and integrity of the Internet's naming and address allocation systems.

They created a working group which convened 2014-2015 to review the use of Public Suffix Lists, and how to impliment them within software, in security, and in language libraries and other systems.  This ultimately resulted in SAC070, an advisory on the use of Public Suffix Lists.

Although it is slightly dated, and not current and entirely applicable to the Mozilla PSL, it does contain good practices and advise.  The list maintainers have migrated management since here to GitHub, have introduced numerous validation and verification steps, and now have in place many of the suggestions and recommendations that were actionable as improvements.

Other suggestions and recommendations were made for those who integrate or use the PSL, and worth a read and consideration, as they were drawn from a pool of security experts that are familiar with architectural and procedural practices that merit some attention.

Please familiarize yourself with their findings and consider them in your use of these lists. 

[SAC070 In Japanese / 日本語](https://www.icann.org/ja/system/files/files/sac-070-ja.pdf) [SAC070 In English](https://www.icann.org/en/system/files/files/sac-070-en.pdf)


### ICANN Office of the Chief Technology Officer (OCTO)
The ICANN OCTO team published a guide for TLD Administrators regarding the Public Suffix List, which is helpful reading that includes actions that TLD Administrators should consider with respect to the Universal Acceptance and the impacts and benefits of monitoring the PSL and maintaining current records.  

[OCTO-11, "The Public Suffix List: A Guide for TLD Administrators"](https://www.icann.org/en/system/files/files/octo-011-18may20-en.pdf)