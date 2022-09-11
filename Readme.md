# Theme

Idea: default styles in [style.css](./style.css), light theme. Define variables for all those needs to be overwritten.
Dynamically local [style.dark.css](./style.dark.css), which contains only overwritten for those variables.

## Points

1. Use javascript to check system preference

    ```javascript
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
        // dark mode
        systemPreferenceDiv.innerText = "Dark Mode";
        isDarkTheme = true;
    }
    ```

1. When it is dark theme, load the css dynamically

    ```javascript
    if (isDarkTheme) { addDarkTheme(); }
    ...
    function addDarkTheme() {
        // Already added.
        let id = 'dark-theme-css';
        let darkThemeCssTag = document.getElementById(id);
        if (!!darkThemeCssTag) {
            return;
        }

        let head = document.getElementsByTagName('head')[0];

        // Creating link element
        let style = document.createElement('link')
        style.href = 'style.dark.css';
        style.type = 'text/css';
        style.rel = 'stylesheet';
        style.id = id;
        head.append(style);
    };
    ```
1. Set the user picker to match the current theme:

    ```javascript
    let targetRadioId = isDarkTheme ? 'dark' : 'light';
    let targetRadio = document.getElementById(targetRadioId);
    targetRadio.checked = true;
    ```

1. All the user to pick a theme:

    ```html
    <div>User overwrite:
      <input type="radio" id='dark' name='pick_theme' value='dark' onchange="chooseTheme(true)" />
      <label for='dark'>Dark Mode</label>
      <input type="radio" id="light" name="pick_theme" value="light" onchange="chooseTheme(false)" />
      <label for="light">Light Mode</label>
    </div>
    ```

Other methods and details in [index.html](./index.html).