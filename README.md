# NgAutoComplete / Example

![](https://raw.githubusercontent.com/sengirab/ng-autocomplete/master/demo.gif)

# Installation

`npm i ng-auto-complete --save`

# Styling !important
First thing to note, i've created this package to be as simple as possible. That's why i don't include any styling,
this is so you could style it the way you want it.

If you like the styling i did for the example .gif shown above, you can copy it from [here.](https://github.com/sengirab/ng-autocomplete/blob/master/src/styles.css) 

# Usage

#### app.module.ts
```typescript
import {BrowserModule} from "@angular/platform-browser";
import {NgModule} from "@angular/core";
import {FormsModule} from "@angular/forms";
import {HttpModule} from "@angular/http";

import {AppComponent} from "./app.component";
import {NgAutoCompleteModule} from "ng-auto-complete";

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        FormsModule,
        HttpModule,
        NgAutoCompleteModule
    ],
    providers: [],
    bootstrap: [AppComponent]
})
export class AppModule {
}
```

#### app.component.ts
```typescript
import {Component, ViewChild} from "@angular/core";
import {CreateNewAutocompleteGroup, SelectedAutocompleteItem} from "ng-auto-complete";
import {NgAutocompleteComponent} from "ng-auto-complete/ng-autocomplete.component";

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
})
export class AppComponent {
    @ViewChild(NgAutocompleteComponent) public completer: NgAutocompleteComponent;
    
    public group = [
        CreateNewAutocompleteGroup(
            'Search / choose in / from list',
            'completer',
            [
                {title: 'Option 1', id: '1'},
                {title: 'Option 2', id: '2'},
                {title: 'Option 3', id: '3'},
                {title: 'Option 4', id: '4'},
                {title: 'Option 5', id: '5'},
            ],
            {titleKey: 'title', childrenKey: null}
        ),
    ];

    constructor() {

    }

    /**
     *
     * @param item
     * @constructor
     */
    Selected(item: SelectedAutocompleteItem) {
        console.log(item);
    }
}

```

#### app.component.html

```html
<ng-autocomplete (selected)="Selected($event)" [classes]="['']"
                     [group]="group"></ng-autocomplete>
```

#Remove selected values
```typescript
public selected: any[] = [];

Selected(item: SelectedAutocompleteItem) {
    this.selected.push(item.item);

    /**
     * Remove selected values from list,
     * selected value must be of type: {id: string(based on GUID's), [value: string]: any}[]
     */
    this.completer.RemovableValues('completer', this.selected)
}
```

#NgAutocompleteComponent Functions
###Note:

<p>I have made all NgAutocompleteComponent and CompleterComponent public, so you could do a lot more than i'll show you<p>
<p>I've documented the functions of which i think their useful:<p>


###Usage
```typescript
@ViewChild(NgAutocompleteComponent) public completer: NgAutocompleteComponent;
```

| Left-aligned | Center-aligned |
| :---         |     :---:      |
| ResetCompleters()   | Resets all rendered completers |
| FindCompleter(key: string)     | Find completer by assigned key |
| RemovableValues(key: string, list: {id: string, [value: string]: any}[]) | Remove options from rendered list (by id) |

#CompleterComponent Functions
###Usage
```typescript
@ViewChild(NgAutocompleteComponent) public completer: NgAutocompleteComponent;
public input = this.completer.FindCompleter('completer');
```

| Left-aligned | Center-aligned |
| :---         |     :---:      |
| ClearValue()   | Clears found completer's input. |
