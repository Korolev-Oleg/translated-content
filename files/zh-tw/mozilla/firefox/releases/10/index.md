---
title: Firefox 10 技術文件
slug: Mozilla/Firefox/Releases/10
translation_of: Mozilla/Firefox/Releases/10
---
{{FirefoxSidebar}}

Firefox 10 shipped on January 31, 2012. This article provides information about the new features and key bugs fixed in this release, as well as links to more detailed documentation for both web developers and add-on developers.

This documentation is not yet complete. Want to help document Firefox 10? See the [list of bugs that need to be written about](http://beta.elchi3.de/doctracker/#list=fx&version=10.0) and pitch in!

> **備註：** Firefox 10 is the first release of this browser with two digits. This may lead to problem with some UA-sniffing scripts. Be sure to check them, and those contained in 3rd-party software you embed in your pages, like libraries. For more information about this, look at the [Firefox goes 2-digit article on hack.mozilla.org](http://hacks.mozilla.org/2012/01/firefox-goes-2-digit-time-to-check-your-ua-sniffing-scripts/).

## Changes for Web developers

### HTML

- The new HTML5 {{ HTMLElement("bdi") }} element, bi-directional isolation, allowing isolation of parts of text with a different directionality has been implemented. This is especially useful when displaying text with an unknown directionality, coming from a database for example, in the middle of text with a known, and potentially, different one.
- You may now specify a fragment of "top" for the {{ htmlattrxref("href", "a") }} attribute to create a link to the top of the page. This used to work, then went away for a while, and now it's back, for compatibility with the HTML5 specification. For example: `<a href="#top">Return to top of page</a>`.

### JavaScript

- The method `WeakMap.set()` now returns _`undefined`_, instead of itself.
- A bug was introduced in regular expression handling in Firefox 7; this has been fixed. See {{ bug(683838) }} if you want the gory details.
- You can no longer use [E4X](/en/E4X) syntax while in [ECMAScript 5 strict mode](/en/JavaScript/Reference/Functions_and_function_scope/Strict_mode) (that is, after `"use strict;"`).

### DOM

#### DOM3 Events

- The DOM Event method [`event.stopImmediatePropagation`](/en/DOM/event.stopImmediatePropagation) has been implemented.
- The mouse events `mouseenter` and `mouseleave` have been implemented.

#### DOM4

- The attribute {{ domxref("document.xmlVersion") }} (which was only gettable and not settable) has been removed as it has been deprecated in the DOM4 specification. The article for {{ domxref("document.xmlVersion") }} now suggests a way to detect whether the document is HTML or XML without using that property.
- The attribute {{ domxref("document.xmlStandalone") }} has been removed as it has been deprecated in the DOM4 specification.
- The attribute {{ domxref("document.xmlEncoding") }} has been removed as it has been deprecated in the DOM4 specification.
- The attribute {{ domxref("text.isElementContentWhiteSpace") }} has been removed as it has been deprecated in the DOM4 specification.
- The method {{ domxref("text.replaceWholeText") }} has been removed as it has been deprecated in the DOM4 specification.
- The method {{ domxref("node.isSameNode") }} has been removed as it has been deprecated in the DOM4 specification. Instead of `node1.isSameNode(node2)`, you can simply use the `===` operator, like this: ` node1 ===`` node2  `.

#### Page Visibility API

- The [Page Visibility API](/en/DOM/Using_the_Page_Visibility_API) has been implemented (prefixed): `document.mozHidden`, `document.mozVisibilityState` are available and the event `mozvisibilitychanged` is sent when the state is modified.

#### Full Screen API

- Support for {{ domxref("document.mozFullScreenEnabled") }} has been added.
- The new {{ cssxref(":-moz-full-screen-ancestor") }} property has been added. This lets you match against elements that are ancestors of an element in full screen mode.

#### Battery API

- Experimental support for {{ domxref("window.navigator.mozBattery") }} has been added (can be enabled setting the preference `dom.battery.enabled` to `true` and will be enabled by default starting with Firefox 11).

#### Canvas

- The [`createPattern()`](/en/DOM/CanvasRenderingContext2D#createPattern%28%29) method now throws an exception if a zero-sized source canvas is specified.
- If you use a non-finite value for any of the numeric parameters to [`putImageData()`](/en/DOM/CanvasRenderingContext2D#putImageData%28%29), the call is now silently ignored instead of throwing an exception, in keeping with the specification.

#### WebGL

- Firefox 10 now supports the [`OES_standard_derivatives`](http://www.khronos.org/registry/webgl/extensions/OES_standard_derivatives/) extension.
- [New preferences have been added](/en/WebGL#WebGL_debugging_and_testing) to help test WebGL code for compatibility with minimally-capable devices on your full development platform.

#### Web Workers

- The attribute `XMLHttpRequest.responseType` and `XMLHttpRequest.response` are now available from inside [Workers](/en/DOM/Worker/Functions_available_to_workers#section_2).
- The [`Worker()`](</en/DOM/Worker#Worker()>) constructor now accepts [data URIs](/en/data_URIs).

#### IndexedDB

Great progress has been made to update IndexedDB to the latest draft specification. This effort will continue in Firefox 11.

- The [`IDBIndex.count()`](/en/IndexedDB/IDBIndex#count) and [`IDBObjectStore.count()`](/en/IndexedDB/IDBObjectStore#count) methods have been added.
- The [`IDBCursor.advance()`](/en/IndexedDB/IDBCursor#advance) method has been added.
- When encountering an unknown optional parameter in [`IDBObjectStore.createIndex()`](/en/IndexedDB/IDBObjectStore#createIndex) or [`IDBDatabase.createObjectStore()`](/en/IndexedDB/IDBDatabase#createObjectStore), Gecko will not fire an exception anymore, but simply ignore it.
- When [`IDBTransaction.abort()`](/en/IndexedDB/IDBTransaction#abort%28%29) is called, all pending [`IDBRequest`](/en/IndexedDB/IDBRequest) have their `errorCode` set to `ABORT_ERROR`.
- The methods [`IDBObjectStore.delete()`](</en/IndexedDB/IDBObjectStore#delete()>) and [`IDBCursor.delete()`](</en/IndexedDB/IDBCursor#delete()>) now set the `result` attribute of the returned [`IDBRequest`](/en/IndexedDB/IDBRequest) to `undefined`.
- The method [`IDBDatabase.setVersion()`](</en/IndexedDB/IDBDatabase#setVersion()>) has been removed as it was removed from the latest spec. The version of the database is given through the [`IDBFactory.open()`](/en/IndexedDB/IDBFactory#open) method which has been updated and the `onupgradeneeded `callback allows the schema of the database to be upgraded. The version itself has been changed from a `DOMString` to an `unsigned long long`. The [`IDBVersionChangeRequest`](/en/IndexedDB/IDBVersionChangeRequest) interface has been removed and replaced by the new [`IDBOpenDBRequest`](/en/IndexedDB/IDBOpenDBRequest) interface.
- The method [`IDBFactory.deleteDatabase()`](/en/IndexedDB/IDBFactory#deleteDatabase%28%29) method has been added.

#### Other

- When the proper MIME type is passed, `image/svg+xml`, [the `DOMParser` now creates a `SVGDocument`](/en/DOM/DOMParser#Parsing_a_SVG_document) when given a string with SVG.
- In the past, when {{ domxref("element.setAttribute()") }} parsed integers, it would report an error if the integer included any non-numeric characters (for example "42foo"). Now it correctly truncates this as the number 42, in accordance with the specification.
- The ESC key no longer incorrectly results in the {{ domxref("window.oninput") }} handler incorrectly getting called.
- The {{ domxref("NameList") }} interface is no longer implemented; it previously had an implementation with no way to actually get access to one.
- The {{ domxref("document.createProcessingInstruction()") }} method now works on HTML documents as well as XML documents. {{ domxref("ProcessingInstruction") }} nodes are still only supported on XML documents, but since nodes can be moved among documents, it's helpful to be able to create them on HTML documents as well.
- The {{ domxref("XMLHttpRequest") }} `responseType` "`moz-json`" [introduced in Firefox 9](/en/Firefox_9_for_developers#DOM) has been updated to the latest draft of the specification and has been unprefixed. See {{ bug("707142#c13") }}

### CSS

- CSS 3D Transforms are now supported. This includes support for the {{ cssxref("transform-style") }}, {{ cssxref("perspective") }}, {{ cssxref("perspective-origin") }} and {{ cssxref("backface-visibility") }} properties, as well as for 3D transform functions in the {{ cssxref("transform") }} and {{ cssxref("transform-function") }} properties. See [Using CSS transforms](/En/CSS/Using_CSS_transforms#3D_specific_CSS_properties) for details.
- Two new values for the CSS property {{ cssxref("unicode-bidi") }} have been added: `-moz-isolation` and `-moz-plaintext`. The `-moz-isolation` value isolates, from a directionality point of view, the element from its environment, letting it have a different directionality. An element with `unicode-bidi:-moz-isolation` behaves like a {{ HTMLElement("bdi") }} element. The `-moz-plaintext` indicates the browser to use the Unicode browser heuristic to determine directionality and not the CSS {{ cssxref("direction") }} property.
- The CSS {{ cssxref("linear-gradient") }} and {{ cssxref("repeating-linear-gradient") }} properties have been updated to support the new `to` syntax and the _magic corner_ algorithm. This allows to give a precise color on the corner of a gradient-filled box.
- The {{ cssxref("text-overflow") }} property's handling of cases in which the box overflows on both sides while the `text-overflow` property is set to overflow on only one [has been corrected](/en/CSS/text-overflow#Gecko_notes).
- Handling of the {{ cssxref("position") }} property on elements inside positioned {{ HTMLElement("table") }} elements [has been fixed](/en/CSS/position#Gecko_notes). **This change will affect layout of pages; however, we now comply with the CSS specification and with other browsers, so this should be easy to fix.**
- Margin collapsing around {{ HTMLElement("table") }} elements has been fixed to match the CSS specification. Previously, table elements' margins would not be collapsed along with other adjacent elements, leading to incorrect layout. **This change will affect layout of pages; however, we now comply with the CSS specification and with other browsers, so this should be easy to fix.**

### SVG

- The {{ SVGElement("mask") }} element has been updated to support both sRGB and linearRGB, and now defaults to sRGB, in compliance with the latest revision of the SVG 1.1 specification.

### Networking

- The HTTP `Accept-Charset` header is no longer sent in HTTP requests. In its absence, servers should respond by sending UTF-8.

### Developer tools

- The {{ domxref("console") }} object has two new methods, {{ domxref("console.time()") }} and {{ domxref("console.timeEnd()") }}, which can be used to set timers on a page.
- The new [Page Inspector](/en/Tools/Page_Inspector) has been added, providing an excellent way to examine and manipulate the HTML and CSS behind your content.

## Changes for Mozilla and add-on developers

For an overview of likely issues that may arise when updating your add-ons to support Firefox 10, see [Updating add-ons for Firefox 10](/en/Firefox/Updating_add-ons_for_Firefox_10).

> **備註：** The old [`PRBool`](/en/PRBool) data type has been retired! Anywhere in the documentation that refers to it now uses the standard C++ `bool` type instead. Documentation will be updated in the future, but for now, just keep this in mind.

### Manifests

- Support for [`<em:strictCompatibility>`](/en/Install_Manifests#strictCompatibility) has been added to the install manifest. It allows add-ons authors to opt in to checking the maximum version of their extension. If set to `true` the add-on will be disabled if the application version is greater than `<em:maxVersion>`. Firefox 10 defaults to add-ons being compatible, regardless of their specified maximum version. This flag overrides that preference. You should set this if your add-on does things that are likely to be broken by Firefox updates, **but not** if your add-on has a binary component, since such add-ons always get strictly checked (remember that binary components must always be recompiled for each major Firefox release).
- If you wish to revert to the old behavior -- that is, to strict compatibility checking for all add-ons, regardless of the value of the `strictCompatibility` flag in their manifests, you can set the `extensions.strictCompatibility` preference to `true`.

### XUL

- Bootstrapped add-ons using a [chrome.manifest](/en/Chrome_Registration) file now have the manifest file registered automatically. See the section [Adding user interface with a chrome.manifest](/en/Extensions/Bootstrapped_extensions#Adding_user_interface_with_a_chrome.manifest) for details.

### XPConnect

- Several new properties and methods have been added to [`Components.utils`](/en/Components.utils), granting access to assorted debugging-related information.

### Interface changes

- The `mozISpellCheckingEngine` and `nsIEditorSpellCheck` interfaces have been updated to allow restartless add-ons to add dictionaries to the spell checker. **XXX need to [update docs](/En/Using_an_External_Spell-checker) on how to actually do this.**
- The `nsIBrowserHistory.lastPageVisited` attribute has been removed.
- The `nsIDocumentViewer` interface has been merged into `nsIContentViewer`.
- The `nsIURIFixup` interface has a new flag, `FIXUP_FLAG_USE_UTF8`, which lets you tell it to use UTF-8 instead of the platform character set, when doing conversions.

### Plug-in changes

- The [new variable `NPNVdocumentOrigin`](/en/Gecko_Plugin_API_Reference/Plug-in_Development_Overview#Working_with_URLs) has been added; this returns the document origin, and is more secure than {{ domxref("window.location") }}.

### Build system changes

- The `--disable-rdf` build option, which actually made it impossible to successfully build, has been removed. Work is ongoing on being able to actually remove RDF support entirely, but at present XUL still requires it to function. See {{ bug(559505) }} for progress on removing the last vestiges of RDF being required.
- The `--disable-smil` build option has been removed.

### See also

- [Firefox 9 for developers](/en/Firefox_9_for_developers)
- [Firefox 8 for developers](/en/Firefox_8_for_developers)
- [Firefox 7 for developers](/en/Firefox_7_for_developers)
- [Firefox 6 for developers](/en/Firefox_6_for_developers)
- [Firefox 5 for developers](/en/Firefox_5_for_developers)
- [Firefox 4 for developers](/en/Firefox_4_for_developers)
- [Firefox 3.6 for developers](/en/Firefox_3.6_for_developers)
- [Firefox 3.5 for developers](/En/Firefox_3.5_for_developers)
- [Firefox 3 for developers](/en/Firefox_3_for_developers)
- [Firefox 2 for developers](/en/Firefox_2_for_developers)
- [Firefox 1.5 for developers](/en/Firefox_1.5_for_developers)
