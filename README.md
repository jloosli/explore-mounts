# Exploring Hugo mounts

## What I'm trying to accomplish:

Import from [modern-normalize](https://github.com/sindresorhus/modern-normalize) `modern-normalize.css` into my
`scss`.

## What I've tried/would like to do

[`config.toml`](config.toml)

```toml
[module]
[[module.imports]]
path = "github.com/sindresorhus/modern-normalize"
disable = false
[[module.imports.mounts]]
source = "./modern-normalize.css"
target = "assets/scss/_modern-normalize.scss"
```

[`assets/scss/style.scss`](assets/scss/style.scss)

```scss
@import 'modern-normalize';
```

### Results from the above attempt
Using the attached [docker-compose.yml](docker-compose.yml) file, when I run either `docker-compose build` or 
`docker-compose server`, I get a generated `css` file that looks like the following:

```css
@import url(/tmp/modules/filecache/modules/pkg/mod/github.com/sindresorhus/modern-normalize@v1.0.0/modern-normalize.css);
```

Which results in the web browser not being able to find that file.

## What does work (although I'd prefer the above)

[`config.toml`](config.toml)

```toml
[module]
[[module.imports]]
path = "github.com/sindresorhus/modern-normalize"
disable = false
[[module.imports.mounts]]
source = "./modern-normalize.css"
target = "static/css/modern-normalize.css" 
```

[`assets/scss/style.scss`](assets/scss/style.scss)

```scss
@import 'modern-normalize.css';
```

### Results from this attempt

The exported css file looks like the following:

```css
@import "modern-normalize.css";
```

Which it finds at `css/modern-normalize.css`.

## Visual results

### modern-normalize imported correctly
![modern-normalize successfully imported](https://github.com/jloosli/explore-mounts/blob/main/static/images/modern-normalize-imported.png?raw=true)

### modern-normalize not imported correctly
![modern-normalize not imported](https://github.com/jloosli/explore-mounts/blob/main/static/images/modern-normalize-not-imported.png?raw=true)