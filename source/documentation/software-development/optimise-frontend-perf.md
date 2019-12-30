# How to optimise frontend performance

You should focus on [frontend performance][] when developing your service’s website. This will improve the user experience of your service by making your website respond faster and work better on all devices.

## Prioritise performance tasks

You can optimise your site’s frontend performance by prioritising tasks that will improve your site speed. Prioritise things you must do (high) over medium or low priority (nice to have) tasks.

For example:

|Priority|Example|Action
|---|---|---|
|High|Position styles correctly|Set styles at the top and scripts at the bottom of a webpage|
||Minimise HTTP requests|Minimise tiling icons, CSS and JavaScript files to reduce size and loading time [HTTP/1.1 only]|
||Compress static resources|Use [minification][] and [Gzip][] to compress CSS and JavaScript code|
||Set correct Headers|Set correct [Cache-Control][] and [ETag][] headers on assets for optimal caching|
|Medium|Look for empty image `src` attributes|Avoid using empty image `src` attributes as some browsers always send requests to them, resulting in additional traffic|
||Minimise DNS lookups|Use fewer third-party domains to reduce the number of DNS lookups per page|
||Maximise parallelisation|Serve static assets from a different subdomain so browsers can download more assets in parallel [HTTP/1.1 only]|
||Investigate [lazy loading][]|For pages with many images, only load images in the immediate browser viewport|
||Investigate the impact of loading multiple [@font-face][] assets|Investigate @font-face assets when dealing with common issues like [FOUT, FOIT and FOFT][]|
|Low|Set images and sprites correctly|Set images and sprites horizontally as it’s easier for browsers to parse|
||Reduce cookie size|Because every cookie is sent with each HTTP request, consider using a cookie-free domain for static assets [HTTP/1.1 only]|
||[AJAX][] requests using JSON|Avoid adding too much data to a JSON Object because this causes performance errors with parsing|
||Investigate using [WebSockets][]|Consider using WebSockets rather than [XMLHttpRequest][], because an HTTP request packet has 1,684 bytes of overhead, compared to 8 bytes for a WebSocket packet|
||Investigate using a service worker| Consider using a service worker to cache critical assets on users machines instead of transferring them over the network

## Automate optimisation

You can automate performance optimisation using tools such as:

- [Gulp][]
- [Grunt][]
- [Broccoli][]
- [npm-scripts][]

You should integrate these tools into your [Continuous Delivery (CD) and Continuous Integration (CI) workflow][] so they automatically run before deployment.

Consider automating common tasks like:

- CSS and JS Linting and optimisation
- CSS and JS Minification
- image optimisation
- sprite and icon generation
- SVG Image optimisation

[Google PageSpeed][] can perform many of these tasks for you.

## Automate testing

You can automate frontend performance testing during deployment using third-party services such as:

- WebPagetest
- Google PageSpeed Insights
- SpeedCurve

You should [set a performance budget][] for your website’s pages. Once you’ve set a performance budget, test to check your website’s pages stay within your budget. There are many tools available to do this, such as:

- grunt-prefbudget
- grunt-pagespeed
- performance-budget
- PSI - PageSpeed Insights with reporting
- Google Lighthouse

## Further reading

You can find out more about improving your website’s frontend performance by reading:

- [Setting a performance budget][]
- [My performance audit workflow][]
- [Front-end performance for web designers and front-end developers][]
- [Improving web app performance with the Chrome DevTools Timeline and Profiles][]
- [Google Web Fundamentals: Optimizing Content Efficiency][]

The Service Manual has more suggestions about [how you can test frontend performance][].

[frontend performance]: https://www.gov.uk/service-manual/technology/how-to-test-frontend-performance
[minification]: http://minifycode.com/
[Gzip]: https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer#text_compression_with_gzip
[Cache-Control]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control
[ETag]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag
[lazy loading]: https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/#what_is_lazy_loading
[@font-face]: https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face
[FOUT, FOIT and FOFT]: https://css-tricks.com/fout-foit-foft/
[AJAX]: https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started
[WebSockets]: https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API
[XMLHttpRequest]: https://xhr.spec.whatwg.org/
[Gulp]: https://gulpjs.com/
[Grunt]: https://gruntjs.com/
[Broccoli]: http://broccolijs.com/
[npm-scripts]: https://css-tricks.com/why-npm-scripts/
[Continuous Delivery (CD) and Continuous Integration (CI) workflow]: https://www.gov.uk/service-manual/technology/deploying-software-regularly
[Google PageSpeed]: https://developers.google.com/speed/pagespeed/module/
[set a performance budget]: https://www.gov.uk/service-manual/technology/how-to-test-frontend-performance#set-a-performance-budget
[Setting a performance budget]: https://timkadlec.com/2013/01/setting-a-performance-budget/
[My performance audit workflow]: https://aerotwist.com/blog/my-performance-audit-workflow/
[Front-end performance for web designers and front-end developers]: https://csswizardry.com/2013/01/front-end-performance-for-web-designers-and-front-end-developers/
[Improving web app performance with the Chrome DevTools Timeline and Profiles]: https://addyosmani.com/blog/performance-optimisation-with-timeline-profiles/
[how you can test frontend performance]: https://www.gov.uk/service-manual/technology/how-to-test-frontend-performance
[Google Web Fundamentals: Optimizing Content Efficiency]: https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/
