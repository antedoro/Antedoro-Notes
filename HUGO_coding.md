## Come migrare da Wordpress a Hugo

[Switching From WordPress To Hugo](https://www.smashingmagazine.com/2019/05/switch-wordpress-hugo/)

[Migrating from WordPress to Hugo](https://davegill.io/blog/migrating-from-wordpress-to-hugo/)

[Migrating my blog from WordPress to Hugo](https://yeokhengmeng.com/2020/04/migrating-my-blog-from-wordpress-to-hugo/)

[Migrating my blog from WordPress to Hugo](https://gomakethings.com/migrating-from-wordpress-to-hugo/)

---

## Come fare un cilo di for con hugo

'
{{ range after 1 (seq 20)}}
{{ end }}
'
oppure 
'
{{ range $index, $num := (seq 20) }}
$indexStartingAt1 := (add $index 1)
{{ end }}

'

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


