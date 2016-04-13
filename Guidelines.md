## Introduction

In order to make the Public Suffix List as current and accurate as possible, we request that TLD registries put in place processes to keep their section of the list current and accurate. This will make sure that all sites within their TLD continue to function fully within modern browsers, in terms of the site owners' ability to set cookies and so on.

In addition, owners of privately-registered domains who themselves issue subdomains to mutually-untrusting parties may wish to be added to the PRIVATE section of the list.

The general procedure to make changes is as follows:

1. Carefully read about the [list format](https://publicsuffix.org/list/#list-format) to see how the list rules are defined.
2. [View the list](https://publicsuffix.org/list/), find your top-level domain (if present), and then check the rules already there for accuracy.
3. If there are any additions, removals or amendments to be made, create a pull request for our Github repo.

Updates can be filed as either pull requests or issues, however a pull request is generally preferred. Pull requests are automatically checked by our test suite, and you can get an immediate feedback whether your submission contains some invalid rules that may cause the patch to be rejected.

Submissions are discussed either in the issue or in the pull request. Each submission requires validation, authentication and approval:

- **Validation**: the patch is validated to make sure it follows the [list format](https://publicsuffix.org/list/).
- **Authentication**: the patch is authenticated to make sure the changes are legit. The exact authorization procedure depends on the type of changes (see below).
- **Approval**: the patch is manually approved and merged. Generally, if the patch is validated and authenticated the approval is granted. However, in some cases we reject the request or encourage the submitter to alter the patch if we feel that the change will negatively impact the experience of the PSL consumers.

## Authentication

### ICANN Domains

These are Top Level Domains (or their direct, affiliated subordinates) that are **delegated by the IANA**, per ICP-3, or new Top Level Domains with a contracting announcement from ICANN (these are in a special section within the ICANN Domains.  

Changes here need to either come from a representative of the registry (authenticated in a similar manner to below) or be from public sources such as a registry website.

### Private Domains

For private domains we need to confirm that the person submitting the request is an authorized representative of the domain owner. **We will not accept patches submitted by third party users of the service**.

Historically, we have been validating the authentication of the request by using the data in the whois response and sending an email to the domain owner. However, this approach doesn't scale very well. Here's the current validation list, in order of preference.

#### DNS Authentication

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

#### Email Authentication

In some circumstances, we may proceed with the email-based validation. However, the email must be clearly associated (generally in the public whois) with all the suffixes included in the pull request. If the pull request contains multiple suffixes and the email doesn't match all of them, then the entire pull request will be rejected.

For large companies we may require a mailing list such as `security@example.com` or administrative email, rather user-specific emails.


## Submit amendments

Follow this procedure to submit a change to the list.

### Understand the list

Carefully read about the [list format](https://publicsuffix.org/list/#list-format) to see how the list rules are defined

[View the list](https://publicsuffix.org/list/), find your top-level domain (if present), and then check the rules already there for accuracy. If you want to submit a private domain, go to the private domain section and find the appropriate position.

### Understand the requirements

Read this page to properly understand the validation/authentication/approval requirements before submitting your request.

### Prepare the change

Prepare your change. Here's some rules to keep in mind:

- Follow the repository conventions

- For a new private domain section, start the change with an header that includes the company information and the submitter email. You must be in control of the submitter email, as we may use it for the authentication. The email must belong to the entity that requests the change (note that you can only modify a private domain section if you are an authorized representative of the company).

   ```
   // Example Company : https://example.com/
   // Submitted by John Doe <security@example.com>
   foo.example.com
   ```

- For a IANA domain, update the header only if you have more relevant references.

- Keep the list of suffix (if more than one) in alphabetical order. Sort first by the TLD, then the first label to the left of the TLD, and so forth. For example, the following is sorted by TLD first (`com`, `invalid`, `net`, `org`, `test`), then within each TLD, sorted by the first label (`example`), then, for entries with more labels, each label is sorted, with shorter entries appearing first:
   ```
   beta.example.com
   alpha.beta.example.com   // alpha.beta has more labels than beta, and thus comes second.
   delta.example.invalid    // invalid sorts between com and net
   beta.example.net
   delta.example.net        // delta sorts after beta, as example and net are the same
   charlie.example.org      // org sorts after net, because sorting is by the right-most label, not the left-most
   alpha.example.test
   ```

### Submit the change

Either open a ticket and paste the change (use the code Markdown formatting), or (recommended) [create a pull request](https://help.github.com/articles/creating-a-pull-request/).

It's recommended to clone and edit the change locally, as you will be able to test the changes before submitting the request. However, if you feel more comfortable, just use the GitHub in-browser editing feature to submit the pull request.

Please provide the following information:

- When submitting private domains, add a brief description of why you want the suffix(es) to be added to the list
- When submitting private domains, provide expected input/output if you want us to help you validating the correctness of the request
- When submitting IANA suffixes, provide the authoritative evidences supporting the change (if you work for the registry, just make that clear)
- Provide extra information useful for the PSL team to handle the pull request

### Test the changes

If you make the changes locally, you can run the test suite before submitting the pull request. Make the change to the list, save the changes and run the following make command:

```
$ make test
```

Check the output for errors.

The tests are also run automatically using Travis CI when you create the pull request. 

![](http://cl.ly/3i312c2L0z1t/Screen%20Shot%202016-03-10%20at%2019.24.26.png)

Please pay attention to the results of the tests. If the tests don't pass, amend your patch accordingly to the error messages.

Patches that don't pass the tests will be rejected.

### Follow up

Please follow up to the ticket. Also make sure that the email you listed in the pull request is valid, as we may use it for validation or private follow ups.
