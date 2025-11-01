# PhimThai Website

Website for PhimThai - Thai Phonetic Keyboard

## Live Site

Once published, this site will be available at:
`https://yourusername.github.io/phimthai-site/`

## Pages

- **index.html** - Main page with macOS download and app information
- **privacy.html** - Privacy policy (required by App Store & Play Store)
- **support.html** - Support, FAQ, and troubleshooting

## Setup GitHub Pages

1. Go to repository Settings
2. Navigate to Pages (under Code and automation)
3. Under "Source", select "Deploy from a branch"
4. Under "Branch", select "main" and "/ (root)"
5. Click Save

Your site will be published at `https://yourusername.github.io/phimthai-site/` within a few minutes.

## TODO Before Publishing

- [ ] Update email addresses in all HTML files (currently `support@example.com`)
- [ ] Update GitHub username in index.html footer link
- [ ] Add PhimThai-1.0.pkg to repository after notarization
- [ ] Update iOS and Android app store links once apps are live
- [ ] Test all links after publishing

## After iOS/Android Launch

Update the platform badges in `index.html`:

```html
<!-- Change from: -->
<a href="#" class="badge">📱 Coming Soon: iOS</a>
<a href="#" class="badge">🤖 Coming Soon: Android</a>

<!-- To: -->
<a href="https://apps.apple.com/app/YOUR_APP_ID" class="badge">📱 Download for iOS</a>
<a href="https://play.google.com/store/apps/details?id=com.fsonntag.thaiphonetic" class="badge">🤖 Download for Android</a>
```

## Local Testing

To test locally, simply open the HTML files in a browser:

```bash
open index.html
# or
open privacy.html
```

## License

MIT License - Same as PhimThai app
