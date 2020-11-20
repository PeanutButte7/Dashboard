<p align="center">
  <img src="https://preview.redd.it/ipih1ypz9a061.png?width=960&crop=smart&auto=webp&s=7ea5651fe6b2c46f2a244ca5a01a2ada7a7d3167g">
</p>

# Dashboard
Welcome to my custom dashboard inspired by the popular [Bento](https://github.com/MiguelRAvila/Bento) theme. This one is build with Vue.js as I plan to expand it later with more custom features and want the flexibility of a component based framework. All links are neatly organized in `locales.json` file so it's simple to change them. Just follow the guide bellow.

## Project setup
* After cloning the repository make sure to run `npm install`. 
* Change links and card names in `locales.json`. If you also need to change icons then you have to edit them directly in `App.vue` for now.
* If you want the dashboard to watch your servers you can setup an account on https://updown.io/ and paste the API key into `servers` field in `locales.json`. Otherwise leave it empty.

* When you are done run `npm run serve` to test the site localy or `npm run build` to build a production version.
* Now you can upload the contents of `/dist` directory to your server or github pages.
