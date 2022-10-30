## Iniziare ad usare Hugo
1. **Creare un nuovo sito:** hugo new site ~/Sites/antedorodesigns
2. **Generate the HTML For the New Site:** hugo --verbose
3. **Avviare il server:**  hugo server --verbose --watch

## Creare un nuovo tema
    Create skeleton : hugo new theme mytheme
    Compilare il file theme.tolm
        vi themes/mytheme/theme.toml
        author = "vincenzo antedoro"
        description = "a minimal working template"
        license = "MIT"
        name = "mytheme"
        source_repo = ""
        tags = ["tags", "categories"]

## Configurare il config.toml
    vi config.toml
    theme = "mytheme"
    baseurl = ""
    languageCode = "en-us"
    title = "mytheme - totally refreshing"
    MetaDataFormat = "toml"

**Generare il sito:** hugo --verbose

**Rimuovere la cartella:** /public: rm -rf public

**Creare un nuovo post:** hugo --verbose new posts/first.md

**Creare un archetipo per ogni contenuto della cartella post:**

    vi themes/zafta/archetypes/post.md
    +++
    Description = ""
    Tags = []
    Categories = []
    +++

**Evitare che l'indirizzo della pagina risulti uguale al percorso delle cartelle ma risulti uguale al nome della pagina:**

	$ vi config.toml
	[permalinks]
		page = "/:title/"
		about = "/:filename/"
