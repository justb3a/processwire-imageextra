# ProcessWire ImageExtra

**Designed for use with ProcessWire 3.x**

## About

This module allows you to add additional informations to an image (for example: title, description, link, orientation and any field you may need).

## Usage

For each instance of an image field the field settings will be extended. Navigate to *Admin > Setup > Fields* and edit the desired field. Click on the Input Tab and click on the **"Image Extra Fields ..."** area.
It extends downwards and reveals a form to set up additional custom fields.

The following fields are available by default:

- **description** - image description (core)
- **disable multi language description**
- **orientation** - image orientation
- **orientation values** - values to use as class names or identifiers for different image orientations
- **link** - image link to internal pages
- **other fields** - here you can add any other field by writing it (separated by comma)

For each of the activated custom fields an own column in the specific table will be created.  
As soon as you added any custom field(s), a table containing all fields appears below.
You can set here a textformatter (e.g. Markdown, Paragraph Stripper, ..) as well as a label text (multi-language) for each field - if you want to. The textformatters have to be installed before.

**Caution:** Just removing a custom field will not erase it, due to data persistence. If you really don't need it anymore you have to delete the column manually.
 
After having added some custom fields to an image field, edit a page which has a template containing this field.
Below each image you get some additional config fields - and for sure it provides multi language support.

## Accessing the values

This is no different than accessing the value of any other field.

```php
$image = $page->image->getRandom();
echo $image->caption;
echo $image->location;
echo $pages->get($image->link)->url;
echo $image->getExtraLabel('location') . ': ' . $image->location;
```

### Get extra field label

```php
// outputs something like: "Location: Munich"
echo $image->getExtraLabel('location') . ': ' . $image->location;

// outputs something like: "Ort: München"
echo $image->getExtraLabel('location', 'de') . ': ' . $image->location;
```

## Setting the values

From the API side you can set the values like this:

```php
$page->setOutputFormatting(false);
$page->images->trackChange('title');
$image = $page->images->getRandom(); // or whatever image you want
$image->title = 'Title in default language';
$image->title($languages->get('fi'), 'Title in Finish');
$image->title($languages->get('de'), 'Title in German');
$page->save();
$page->setOutputFormatting(true);
```
