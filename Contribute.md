# Contribution Guidelines

In order to make the Public Suffix List as current and accurate as possible, we request that TLD registries put in place processes to keep their section of the list current and accurate. This will make sure that all sites within their TLD continue to function fully within modern browsers, in terms of the site owners' ability to set cookies and so on.

In addition, owners of privately-registered domains who themselves issue subdomains to mutually-untrusting parties may wish to be added to the PRIVATE section of the list.

The general procedure to make changes is as follows:

1. Carefully read about the [list format](https://publicsuffix.org/list/#list-format) to see how the list rules are defined.
2. [View the list](https://publicsuffix.org/list/), find your top-level domain (if present), and then check the rules already there for accuracy.
3. If there are any additions, removals or amendments to be made, create a pull request for our Github repo.

Updates can be filed as either pull requests or issues, however a pull request is generally preferred. Pull requests are automatically checked by our test suite, and you can get an immediate feedback whether your submission contains some invalid rules that may cause the patch to be rejected.

Submissions are discussed either in the issue or in the pull request. Each submission requires validation, authentication and approval:

- **Validation**: the patch is validated to make sure it follows the [list format](https://publicsuffix.org/list/).
- **Authentication**: the patch is authenticated to make sure the changes are legit. The exact authentication procedure depends on the type of changes (see below).
- **Approval**: the patch is manually approved and merged. Generally, if the patch is validated and authenticated the approval is granted. However, in some cases we reject the request or encourage the submitter to alter the patch if we feel that the change will negatively impact the experience of the PSL consumers.

## Authentication

### ICANN Domains

These are Top Level Domains (or their direct, affiliated subordinates) that are **delegated by the IANA**, per ICP-3, or new Top Level Domains with a contracting announcement from ICANN (these are in a special section within the ICANN Domains.  

Changes here need to either come from a representative of the registry (authenticated in a similar manner to below) or be from public sources such as a registry website.

### Private Domains

For private domains we need to confirm that the person submitting the request is an authorized representative of the domain owner. **We will not accept patches submitted by third party users of the service**.

Historically, we have been validating the authentication of the request by using the data in the whois response and sending an email to the domain owner. However, this approach doesn't scale very well. Here's the current validation list, in order of preference.

#### DNS Validation

For each suffix included in the patch, add a corresponding DNS TXT record called `_psl` that contains the link to the PR.

For example, if you submit the following patch:

```diff
+// Company : http://www.example.com
+// Submitted by John Doe <john@example.com>
+alphaexample.com
+foo.betaexample.com
+*.gammaexample.com
```

Then we expect to find the following DNS records (assuming the pull request ID is 100):

```
$ dig TXT _psl.alphaexample.com
https://github.com/publicsuffix/list/pull/100

$ dig TXT _psl.foo.betaexample.com
https://github.com/publicsuffix/list/pull/100

$ dig TXT _psl.gammaexample.com
https://github.com/publicsuffix/list/pull/100
```

#### Email Validation

In some circumstances, we may proceed with the email-based validation. However, the email must be clearly associated (generally in the public whois) with all the suffixes included in the pull request. If the pull request contains multiple suffixes and the email doesn't match all of them, then the entire pull request will be rejected.

For large companies we may require a mailing list such as `security@example.com` or administrative email, rather user-specific emails.

## Submitting