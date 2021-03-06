# Zotero
Zotero synchronization to Notion is a core component of NotionSci.
Currently, only one way References and Collections sync is supported.

## Setting up Connection
It is highly encouraged to separate api keys for certain library scopes. 
If you need to access multiple Zotero libraries you can create a [separate profile](configuration.md#profiles) for each.

To obtain your Zotero api credentials you need to follow the following steps:

1. You'll need the ID of the personal or group library you want to access:
    - Your **personal library ID** is available [here](https://www.zotero.org/settings/keys), in the section `Your userID for use in API calls`
    - For **group libraries**, the ID can be found by opening the group's page: `https://www.zotero.org/groups/groupname`, and hovering over the `group settings` link. The ID is the integer after `/groups/`
2. You'll also need<sup>†</sup> to get an **API key** [here][https://www.zotero.org/settings/keys/new]
3. Are you accessing your own Zotero library? `library_type` is `'user'`
4. Are you accessing a shared group library? `library_type` is `'group'`. 

Update the configuration with the obtained credentials:

```yaml
...
connections:
  ...
  zotero:
    library_id: '123456'
    library_type: 'user'
    token: ''
```

> [→ Learn more about Zotero API authorization](https://www.zotero.org/support/dev/web_api/v3/basics#authentication).

## Synchronization
> This sections assumes you already have a working Notion connection [→ See Docs](zotero.md#setting-up-connection).

### Duplicating the Project Template
To get started with synchronization your workspace needs to have a page with the [Zotero Library Template](https://efficacious-alarm-7cc.notion.site/Zotero-Library-908bf67ef61048b79a1a10dfa5826302).
You can _duplicate_ it either manually or if you have [Unofficial API](notion.md#unofficial-api) set up you can run the following command:

```bash
notionsci sync zotero template <parent page url or id>
```

Usage:
```bash
Usage: python -m notionsci sync zotero template [OPTIONS] PARENT

  Duplicates the standard Zotero Library template page to your workspace under
  the given parent page

  PARENT: Destination parent page ID or url

Options:
  --help  Show this message and exit.
```

### Collections Sync (One Way)
It is possible to sync Zotero Collection tree to Notion. To do this you need to pass the url of your _"Zotero Collections"_
page to the following command:

```bash
notionsci sync zotero collections <url or id of the cloned library template page>
```

Usage:
```bash
Usage: python -m notionsci sync zotero collections [OPTIONS] TEMPLATE

  Starts a one way Zotero references sync to Notion

  TEMPLATE: Cloned template page ID or url

Options:
  --force  Ensures up to date items are also pushed to Zotero
  --help   Show this message and exit.
```

### References Sync (One Way)
To synchronize your references (Papers, Books, Articles, etc.) you need to pass url of your _"Zotero References"_
page to the following command.

```bash
notionsci sync zotero refs <url or id of the cloned library template page>
```

To include the reference to collection relations you can also specify the collections database.

```bash
notionsci sync zotero refs <url or id of the cloned library template page>
```

Usage:
```bash
Usage: python -m notionsci sync zotero refs [OPTIONS] TEMPLATE

  Starts a one way Zotero references sync to Notion

  TEMPLATE: Cloned template page ID or url

  When collecitons option is specified Unofficial Notion Api access is
  required

Options:
  --force                 Ensures up to date items are also pushed to Zotero
  --help                  Show this message and exit.

```




