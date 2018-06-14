# PrimoFeaturesJSON

`features.json` is a file which lists the various add-ons available for installation through Primo-Studio.

The file consists a JSON-Array which holds JSON-Objects. Each object in the array is called a descriptor and defines a single add-on.

Example descriptor:
```
	{
		"face": "https://pbs.twimg.com/profile_images/905906120794963968/lHQ0ivpW_400x400.jpg",
		"notes": "Add a nav bar underneath the search bar to provide additional links in the primo-explore UI",
		"who": "NYU Libraries",
		"what": "primo-explore-search-bar-sub-menu",
		"linkGit": "https://github.com/NYULibraries/primo-explore-search-bar-sub-menu",
		"npmid": "search-bar-sub-menu-studio",
		"version": "0.0.4",
		"hook": "prm-search-bar-after",
		"config": {
			"multiple":5,
			"form":
			[
				{"key":"name"},
				{"key":"description"},
				{"key":"action"},
				{"key":"iconSet", "templateOptions":{"label": "icon set"}},
				{"key":"iconName", "templateOptions":{"label": "icon name"}},
				{"key":"cssClasses"},
				{"key":"show_xs"}
			]
		}
	}
```

## Descriptor

A descriptor is a JSON-Object consisting the following fields :

| name | type | usage |
|------|-------------|--------|
| `face` | string: required | URL of image icon to be placed next to add button |
| `what` | string: required | Tilte of add-on |
| `notes` | string: required | Brief description of add-on |
| `linkGit` | string: required | URL link for github of add-on |
| `npmid` | string: required | ID of add-on as published on NPM |
| `version` | string: required | Version of add-on to be installed from NPM. Necessary in order to update add-on in Primo Studio|
| `hook` | string: required | name of hook where want to place add-on. E.g: prm-search-bar-after  
| `config` | JSON-Object: optional | Object defining a form that will be opened in Primo Studio where users can enter configuration parameters for add-on. See Below.  |


### 'config' field

The config field of a descriptor is optional and if added will cause Primo-Studio to open a form prompting user to enter the requested parameters when installing the add-on. 
'config' is a JSON-Object consisting the following fields: 

| name | type | usage |
|------|-------------|--------|
| `multiple` | Number: optional default:1 | Max number of forms that are able to be set by the user for the add-on.  e.g: Each form defines a link that will be placed under the search bar and we want to allow up to 5 links.|
| `form` | JSON-Array: required | Json-Array where each element is a JSON-Object defining an input field in the form. See below.  |

The form field is JSON-Array where each element is a JSON-Object defining a single input field in the form. e.g:  
```
    [
		{"key":"name"},
		{"key":"description"},
		{"key":"action"},
		{"key":"iconSet", "templateOptions":{"label": "icon set"}},
		{"key":"iconName", "templateOptions":{"label": "icon name"}},
		{"key":"cssClasses"},
		{"key":"show_xs"}
    ]
```

The simplest example for defining a form field is adding only a key parameter. e.g:  `````{"key":"name"}`````. In this case the form will consist of a field whose title is "name". The parameter will be accessed in the add-on code through the key "name".

If you would like to define a field whose title and key are different you could define the following object for example:  
```{"key":"iconSet", "templateOptions":{"label": "icon set"}}```

For additional form field options see: https://github.com/formly-js/angular-formly-templates-bootstrap
