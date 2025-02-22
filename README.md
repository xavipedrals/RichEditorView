# RichEditorView

NOTE: This is the same as the forked repo but I added my custom CSS from sources since it was not possible to do otherwise

-------

This is the Swift 5 version of [cjwirth/RichEditorView](https://github.com/cjwirth/RichEditorView) using WKWebView that **added several** awesome functionalities.

Table of Contents:
- Usage Instructions
- Added Features
- Credits and License

-------

### Usage Instructions:

You can use SPM to install this package. If you're using Pods or Carthage,
since I haven't created a package for those yet, you'll need to do this manually.

1. In order to import the RichEditorView package, you need to create a new group/folder by going to the bottom left of XCode and clicking on the + button. Create a new group called RichEditorView. 
2. Then, manually create new files and copy and paste accordingly from the RichEditorView directory in the source code. _There is currently no plan to go to CocoaPods or Carthage or any other package manager._ 
3. For resources, if you download this repository via ZIP and then unzip the file, you can right click on YOUR newly created Resources directory and selecting "Add Files to" then select the Resource files from the unzipped package. DO NOT USE Assets!!!

---

### Added Features:

Most features are the same from the [parent repo](https://github.com/cjwirth/RichEditorView), but I have added some other functionalities and some directions in the sample. Other features can be found in cjwirth's repo.

- Checkbox
- Offline & Server-based Image and Video functionality
- Tables ([with editing functionality](https://github.com/YoomamaFTW/RichEditorView/pull/5#issuecomment-592952190))

The following edited features assumes you have a property `let editorView = RichEditorView()`

1. You can get selected text by doing `editorView.getSelectedText`
2. runJS and other functions in the RichEditorView does NOT work like cjwirth's. This is due to the JavaScript bridging for WKWebView; unlike WK, UIWebView had a string be returned. In order to run JavaScript and other functionalities return `Void`, you must do the following:
```
editorView.getSelectedText() { r in
    // r is just a variable.
}
```
or 
```
editorView.runJS("document.getElementById('editor')") { r in 
    print(r)
}
```
**NOTE That these might run asynchronously. This might be due to WKWebView's memory efficiency feature. Don't quote me on that though, since I'm not too sure if that's true. Just an observation.**
This is because the function is: `public func getSelectedText(handler: @escaping (String) -> Void)`. Notice the `(String) -> Void`. The variable `r` is the string value returned by JavaScript.

3. The insertLink functionality has also changed. Normal <a> tags in HTML are layed out like this: `<a href="https://github.com/" title="GitHub">The TEXT that user sees</a>`. When you insert a link, the following arguments are required: href and text. **If there is a range selection, the text in the range selection will be cleared!**
4. Dark mode is included via the CSS and HTML files.

---

### Credits and License

License is under BSD-3 Clause

cjwirth - Original iOS-RichEditorView Creator

C. Bess - WKWebView Support

YoomamaFTW - Repository Maintainer

Andrew-Chen-Wang - Repository Maintainer
