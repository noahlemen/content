---
title: XMLSerializer
slug: Web/API/XMLSerializer
page-type: web-api-interface
browser-compat: api.XMLSerializer
---

{{APIRef("XMLSerializer")}}

The `XMLSerializer` interface provides the {{domxref("XMLSerializer.serializeToString", "serializeToString()")}} method to construct an XML string representing a {{Glossary("DOM")}} tree.

> [!NOTE]
> The resulting XML string is not guaranteed to be well-formed XML.

## Constructor

- {{domxref("XMLSerializer.XMLSerializer", "XMLSerializer()")}}
  - : Creates a new `XMLSerializer` object.

## Instance methods

- {{domxref("XMLSerializer.serializeToString", "serializeToString()")}}
  - : Returns the serialized subtree of a string.

## Examples

### Serializing XML into a string

This example just serializes an entire document into a string containing XML.

```js
const s = new XMLSerializer();
const str = s.serializeToString(document);
saveXML(str);
```

This involves creating a new `XMLSerializer` object, then passing the {{domxref("Document")}} to be serialized into {{domxref("XMLSerializer.serializeToString", "serializeToString()")}}, which returns the XML equivalent of the document. `saveXML()` represents a function that would then save the serialized string.

### Inserting nodes into a DOM based on XML

This example uses the {{domxref("Element.insertAdjacentHTML()")}} method to insert a new DOM {{domxref("Node")}} into the body of the {{domxref("Document")}}, based on XML created by serializing an {{domxref("Element")}} object.

> [!NOTE]
> In the real world, you should usually instead call {{domxref("Document.importNode", "importNode()")}} method to import the new node into the DOM, then call one of the following methods to add the node to the DOM tree:
>
> - The {{domxref("Element.append()")}}/{{domxref("Element.prepend()")}} and {{domxref("Document.append()")}}/{{domxref("Document.prepend()")}} methods.
> - The {{domxref("Element.replaceWith")}} method (to replace an existing node with the new one)
> - The {{domxref("Element.insertAdjacentElement()")}} method.

Because `insertAdjacentHTML()` accepts a string and not a `Node` as its second parameter, `XMLSerializer` is used to first convert the node into a string.

```js
const inp = document.createElement("input");
const XMLS = new XMLSerializer();
const inp_xmls = XMLS.serializeToString(inp); // First convert DOM node into a string

// Insert the newly created node into the document's body
document.body.insertAdjacentHTML("afterbegin", inp_xmls);
```

The code creates a new {{HTMLElement("input")}} element by calling {{domxref("Document.createElement()")}}, then serializes it into XML using {{domxref("XMLSerializer.serializeToString", "serializeToString()")}}.

Once that's done, `insertAdjacentHTML()` is used to insert the `<input>` element into the DOM.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Parsing and serializing XML](/en-US/docs/Web/XML/Guides/Parsing_and_serializing_XML)
- {{domxref("DOMParser")}}
