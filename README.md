# Hugo Apéro

**See the demo site [here](https://hugo-apero.netlify.com)**

**Read the docs [here](https://hugo-apero-docs.netlify.com)**

**Read it's basic template [here](https://github.com/hugo-apero/iyo-apero)**.

# Fixes while dealing with Hugo Apéro

- xaringanextra panelset HTML solution by removing all indentation from the panelset tags

- `MathJax` needs to be manually set up with Hugo Apéro
  Solution: <https://github.com/hugo-apero/hugo-apero/issues/38> _Comment from july 6._

- **Custom theme** 
  Create a folder `assets` in /my-portfolio/ and include a scss file for the custom theme.

- **Include custom JavaScript code**  
  Add them in the `footer.html` where Yihui's MathJax script was inserted.