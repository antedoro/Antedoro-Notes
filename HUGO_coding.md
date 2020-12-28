## Come migrare da Wordpress a Hugo

[Switching From WordPress To Hugo](https://www.smashingmagazine.com/2019/05/switch-wordpress-hugo/)

[Migrating from WordPress to Hugo](https://davegill.io/blog/migrating-from-wordpress-to-hugo/)

[Migrating my blog from WordPress to Hugo](https://yeokhengmeng.com/2020/04/migrating-my-blog-from-wordpress-to-hugo/)

[Migrating my blog from WordPress to Hugo](https://gomakethings.com/migrating-from-wordpress-to-hugo/)

---

## Come fare un ciclo di for con hugo

{{ range after 1 (seq 20)}}
  //eseguire un comando
{{ end }}


oppure 

  '{{ range $index, $num := (seq 20) }}
    $indexStartingAt1 := (add $index 1)
  {{ end }}'



---

## Come stabilire il livello di una TOC (Table of Content via markup con goldfield)

  '
  [markup.tableOfContents]
  
    endLevel = 3
    
    ordered = false
    
    startLevel = 2
    '
    
   ---

## Usare un css particolare per una pagina
I am trying to use the Page Resources feature in order to have a specific css style file for a given page.
I did it as follows:

    adding the resource in the page bundle with the frontmatter of the page

resources:
  - src: test.css
    title: style

and adding the file test.css in the page directory.
Note that this file should be in addition of the basic style of the main theme

    in the single layout I put the following code

{{ with $.Resources.GetMatch "**.css*" }}
{{ $style := . | minify | fingerprint }}
<link type=text/css rel="stylesheet" href="{{ $style.Permalink }}">
{{ end }}

---

## Come contare il numero di parole in un .Content
**<p>Numero di parole: {{.FuzzyWordCount}}</p>**

# My Hugo cheat sheet (by https://dev.to/ohhelloana)


## The if/else

`{{ if }} // something{{ else }} //something{{ end }}`

## How to check if a value is equal to something

`{{ if eq value_1 value_2 }}`

## How to check if a value is lower than something

`{{ if lt value_1 value_2 }}`

## How to check if a value is greater than something

`{{ if gt value_1 value_2 }}`

## How to combine two checks

This example checks if a value is lower than 5 and greater than 1.

`{{ if and (lt $currentIndex 5) (gt $currentIndex 1) }}`

## How to add a class based on what page you're on

I wanted to add a specific class to a page called "Privacy policy". This page was created inside my content folder and I named its folder privacy-policy and inside it I created an _index.md. The frontmatter of the .md file has a title. Something like: title: Privacy Policy.

I want a specific class to be added to an element when I visit this particular page.

`<main class="{{ if eq .Name `Privacy Policy` }}privacy{{ end }}" id="main"> My content</main>`

## How to update aria-current in a menu

This particular example assumes we're iterating on a menu set in the config.

`<nav aria-label="Main menu"> <ul> {{ $currentPage := . }} {{ range .Site.Menus.main }} <li> <a aria-current="{{if or ($currentPage.IsMenuCurrent `main` .) ($currentPage.HasMenuCurrent `main` .)}}true{{else}}false{{end}}" href="{{ .URL }}" title="{{ .Title }}">{{ .Name }}</a> </li> {{ end }} </ul></nav>`

## How to only render something if there is more than one page in a section.

This example assumes we have a section called "latest" that has some posts inside it.

`{{ $news := where .Site.RegularPages "Section" "latest" }} {{ $postCount := len $news }}{{ if gt $postCount 0 }}    <section> {{.Title}}    </section>{{end}}`

## How to only show the latest three posts of a section

This example assumes we have a section called "latest" that has some posts inside it.

`{{ $news := where .Site.RegularPages "Section" "latest" }} <ul> {{ range first 3 $news }} <li>{{.Title}}</li> {{ end }}</ul>`

## How to create a collection of posts that have a certain param and value

This example wants to collect all the posts inside a section that have a specific param defined in the frontmatter.For this example, let's assume that we're looking for all the posts inside a section called "latest" that have type: summary.

`{{ $services := where .Site.RegularPages "Section" "latest" }} {{ $finalList := where $services "Params.type" "summary" }}`

## How to create a collection of posts that match a certain value

This example creates a variable called test that iterates over the pages inside a section called case-studies that have the value of draft as false.

`{{$test := where (where .Site.RegularPages "Section" "case-studies") ".Params.draft" false }}`

## How to range and order by the value of a param

This example assumes that a page has order in the frontmatter and a number.

`{{ $services := where .Site.RegularPages "Section" "latest" }}{{ range $services.ByParam "order" }} // your content{{ end }}`

## How to replace a character with something else

I had a specific situation where I had to replace "_" with a blank space in a couple of words .

`{{ replace $tag "_" " "}}`

## How to get the content of an _index.md inside a partial

Imagine you have a partial (like a banner) and could like to bring the content of the index of a section to it (in this case, for example an "about" page).

`{{ with .Site.GetPage "/about" }} {{ .Content }}{{ end }}`

## How to get Pages that have a value that resolves into false

This example collects all the pages inside a section that have the value "false" for draft.

`where .Pages ".Params.draft" false`

## How to show a list and add commas

This example attempts to re-create something like the following:

"Animals that are very chill: capybaras, tortoise, dogs."

`  <div> <p>Animals that are very chill: {{ $list := (where .Site.Pages "Section" "animals") }} {{ $len := (len $list) }} {{ range where .Site.Pages "Section" "animals" }} {{ range $index, $element := .Pages }} {{ $currentIndex := (add $index 1)}} {{ $currentLength := (sub $len 1 )}} {{.Title}}{{ if eq $currentIndex $currentLength }}. {{else}}, {{end}} {{ end }} {{ end }} </p> </div>`

## Iterate inside a section and combine options

Assuming you're adding this to the list.html of a section, this example shows how to get all the pages of a section that have the param draft as false and putting them in reverse chronological order.

`{{ range ((where .Pages ".Params.draft" false).ByParam "order").Reverse }}`

I think these are my most used logic examples that I needed to look up when I first build some websites using Hugo. I will update this if I remember anything else.

## Easy way to serve responsive images with Hugo

`
{{ image := .Resources.ByType “image” }}

{{ with $image }}

{{ range $index, $image := . }}

{{ if eq index 0}} {{ partial "imghp" (dict "Site" .Site “image” $image) }}

{{ end }}

{{ end }}

{{ end }}

`
## Aggiungere un css custom

This is a common problem when users try to customize a theme. In some of my themes I include an option to easily insert custom stylesheets. Maybe you can do a pull request to add the following scheme to the theme:

Inside the config file I assign an array to a variable:

`
[params]
    custom_css = ["css/foo.css", "css/bar.css"]`

You can reference as many stylesheets as you want. Their paths need to be relative to the static folder.

Inside the header partial you can include every custom stylesheet from above beside the original one:

`
{{ range .Site.Params.custom_css -}}
    <link rel="stylesheet" href="{{ . | absURL }}">
{{- end }}
`

This way you don’t touch the header partial at all but you’re still able to overwrite CSS classes.

## Usare un particolare css per un particolare post/page

A perhaps more flexible solution for themes would be add an empty “extra-in-head.html” partial. This way, users can put anything into the head by overriding “extra-in-head.html”.

It may for example be that for performance reasons, it is desired to include the css directly in the HTML, thereby eliminating a server request.

Or it may be that the user want to include some css on a specific page. He can then create an “extra-in-head.html” partial which includes the CSS specified in the frontmatter, ie something like this:

`
frontmatter:

+++
css = "contact"
...
`

extra-in-head.html:


`
{{ if eq .Params.css "contact"}}
{{ template "css/contact.html" }}
{{ end }}

{{ if eq .Params.css "about"}}
{{ template "css/about.html" }}
{{ end }}

layouts/css/contact.html:

<style>
  h1 {
    margin: 40px;
  }
</style>
`



