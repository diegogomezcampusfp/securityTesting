# VERSIÓN Y SEGURIDAD

<h2> Toda la info la saco de la página oficial: https://angular.io/guide/security </h2>

# Angular versioning
Angular version numbers indicate the level of changes that are introduced by the release. This use of semantic versioning helps you understand the potential impact of updating to a new version.

Angular version numbers have three parts: major.minor.patch. For example, version 7.2.11 indicates major version 7, minor version 2, and patch level 11.

The version number is incremented based on the level of change included in the release.

# Seguridad para Angular
<h2> Preventing cross-site scripting (XSS)  </h2>
Cross-site scripting (XSS) enables attackers to inject malicious code into web pages. Such code can then, for example, steal user and login data, or perform actions that impersonate the user. This is one of the most common attacks on the web.

To block XSS attacks, you must prevent malicious code from entering the Document Object Model (DOM). For example, if attackers can trick you into inserting a <script> tag in the DOM, they can run arbitrary code on your website. The attack isn't limited to <script> tags —many elements and properties in the DOM allow code execution, for example, <img alt="" onerror="..."> and <a href="javascript:...">. If attacker-controlled data enters the DOM, expect security vulnerabilities.

<h2> Angular's cross-site scripting security model  </h2>
To systematically block XSS bugs, Angular treats all values as untrusted by default. When a value is inserted into the DOM from a template binding, or interpolation, Angular sanitizes and escapes untrusted values. If a value was already sanitized outside of Angular and is considered safe, communicate this to Angular by marking the value as trusted.

Unlike values to be used for rendering, Angular templates are considered trusted by default, and should be treated as executable code. Never create templates by concatenating user input and template syntax. Doing this would enable attackers to inject arbitrary code into your application. To prevent these vulnerabilities, always use the default Ahead-Of-Time (AOT) template compiler in production deployments.

An extra layer of protection can be provided through the use of Content security policy and Trusted Types. These web platform features operate at the DOM level which is the most effective place to prevent XSS issues. Here they can't be bypassed using other, lower-level APIs. For this reason, it is strongly encouraged to take advantage of these features. To do this, configure the content security policy for the application and enable trusted types enforcement.

<h2> Direct use of the DOM APIs and explicit sanitization calls </h2>
Unless you enforce Trusted Types, the built-in browser DOM APIs don't automatically protect you from security vulnerabilities. For example, document, the node available through ElementRef, and many third-party APIs contain unsafe methods. Likewise, if you interact with other libraries that manipulate the DOM, you likely won't have the same automatic sanitization as with Angular interpolations. Avoid directly interacting with the DOM and instead use Angular templates where possible.

For cases where this is unavoidable, use the built-in Angular sanitization functions. Sanitize untrusted values with the DomSanitizer.sanitize method and the appropriate SecurityContext. That function also accepts values that were marked as trusted using the bypassSecurityTrust … functions, and does not sanitize them, as described below.
