# GoogleColabNameError
This is to test an error found in Google Colab https://github.com/googlecolab/colabtools. Colab Notebook Meta-data Name attribute error.


* Original Notebook: https://github.com/UmerFakher/GoogleColabNameError/blob/main/Original.ipynb
* Copied Notebook: https://github.com/UmerFakher/GoogleColabNameError/blob/main/Different_Copy.ipynb

## Steps to recreate issue

If we have a notebook, Original.ipynb and we do the following:

* File > Save a copy to GitHub
* and changing the name to Different_Copy.ipynb

## Issue

You can try to open (Different_Copy.ipynb)[https://github.com/UmerFakher/GoogleColabNameError/blob/main/Different_Copy.ipynb] by clicking the link and clicking open in Google Colab and you can see that it opens Original.ipynb instead.

OR

You can also try opening Different_Copy.ipynb manually by going to https://colab.research.google.com/ going to GitHub tab and you will see the following:

![image](https://user-images.githubusercontent.com/66469756/117185658-faa7c080-add1-11eb-9cdc-8283dfc2e23c.png)

Opening this will then incorrectly open Original.ipynb instead of Different_Copy.ipynb.
![image](https://user-images.githubusercontent.com/66469756/117185930-4490a680-add2-11eb-8f7d-fc40a58681c7.png)

**Colab will not open the copied notebook at all** and only open the Original.ipynb incorrectly somehow links to it.

## Why the issue occurs?

**On closer examination of the html code of Different_Copy.ipynb https://github.com/UmerFakher/GoogleColabNameError/blob/main/Different_Copy.ipynb?short_path=fde6b82
we can see in the meta-data below that the "name" is "Original.ipynb":**

```html
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "Original.ipynb",
      "provenance": [],
      "authorship_tag": "ABX9TyNmlPK/SLs2ETtuOlDhsEgM",
      "include_colab_link": true
    },
```

This causes the issue so when you open any copy of some ipython notebook in Colab, it will always open the original due to its meta-data indicating this.


![image](https://user-images.githubusercontent.com/66469756/117186361-a5b87a00-add2-11eb-9ec0-291af63589b1.png)

**Please note I can't access Different_Copy.ipynb as a result** so it hasn't been run. The notebook can be opened locally if not using colab and as a result this could cause quite a headache to any user.

## Here is an example of someone I helped fix this problem for https://github.com/googlecolab/colabtools/issues/1993

## Solution

**This means you have to manually change the name variable in the notebook code to view it in Colab if it has been copied from another notebook through Save a copy to GitHub" (or even if you have used colab with that notebook at some point and rename it in the future, then the redudant name attribute in the meta-data will stay and cause errors)**

To fix it Colab needs to make sure when you rename a notebook/save a copy to GitHub, it changes the meta-data name as well, or since that may not be possible if you rename it outside of Colab, then perhaps they should remove that redundant "name" attribute meta-data
