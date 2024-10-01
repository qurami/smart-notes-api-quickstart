# Smart Notes Embeddable Virtual Tutor QuickStart

The aim of this document is to provide developers with all the pieces of information they need to integrate Smart Notes Embeddable Virtual Tutor in their application.

## Table of Contents

- [Overview](#overview)
- [Integrate Embeddable Virtual Tutor](#integrate-embeddable-virtual-tutor)

## Overview

Smart Notes Embeddable Virtual Tutor provide partners with the ability to integrate the Smart Notes Virtual Tutor in their own application.

To get access to the Embeddable Virtual Tutor you must first purchase a Smart Notes license.

## Integrate Embeddable Virtual Tutor

1. Login into [Smart Notes Manager](https://manager.smart-notes.extrai.app) app, open the side menu and click on `Embed Virtual Tutor`, then follow the instructions to create a new Embeddable Virtual Tutor.

2. After configuring the Embeddable Virtual Tutor navigate to Embedding tab and copy the Embedding code.

3. In the Embedding code replace the following variables:

Variable | Description | Allowed values
-------- | ----------- | --------------
<LOCALE_LANGUAGE_CODE> | Specifies the language of the Embeddable Virtual Tutor's interface. This does not affect the response language of the Virtual Tutor. | `de` (German), `en` (English), `es` (Espagnol), `fr` (French) or `it` (Italian)
<CONTENT_ID(optional)> | The ID of the content to be preselected in the Embeddable Virtual Tutor. | Must be retrieved via the public API [getContents](https://github.com/qurami/smart-notes-api-quickstart#get-the-list-of-contents). Optional; if you don't need to preselect a content, remove this variable from the Embedding code.
<TOKEN> | The token related to the company guest user, which will be used to log the guest user into the Embeddable Virtual Tutor. | Must be generated using the public API [genTokenForEmbeddableVirtualTutorGuest]().
