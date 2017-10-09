[![forthebadge](http://forthebadge.com/images/badges/uses-js.svg)](http://forthebadge.com)


# JavaScript


## Table of Contents

1. [Definitions](#definitions)
1. [Basic Concepts](#concepts)
1. [Calling DOM APIs Directly](#dom)


## Definitions

## Basic Concepts

## Calling DOM APIs Directly


- **Working with the ElementRef directly (not recommended):**

	```javascript

  import { ElementRef } from '@angular/core';

  export class TableComponent implements {

    constructor(

      private _elRef: ElementRef

    ) {

      _elRef.nativeElement.querySelector('input').focus();

    }

  }

	```

- **Working with ViewChild and local variable (recommended):**

	```javascript

  import { AfterViewInit, ElementRef, Renderer2 } from '@angular/core';

  export class TableComponent implements AfterViewInit {

    constructor(

      private _elRef: ElementRef,
      private _renderer: Renderer2,

    ) {}

    @ViewChild('myInput') input : this_elRef;
    @ViewChild('myContainer') container : this_elRef;

    ngAfterViewInit() {

      this.onInputFocus();
      this.updateContainer();

    }

    onInputFocus() {

      this_renderer.invokeElementMethod(this.input.nativeElement, 'focus');

    }

    updateContainer() {

      this._renderer.addClass(this.container.nativeElement, '--fullwidth');

    }

  }

	```

- **Working with the ViewContainerRef directly (not recommended):**

  ```javascript

  import { AfterViewInit, ViewContainerRef } from '@angular/core';

  export class TableComponent implements AfterViewInit {

    constructor(

      private _vcRef: ViewContainerRef

    ) {}

    ngAfterViewInit() {

      this.updateContainer();

    }

    updateContainer() {

      this._vcRef.element.nativeElement.classList.add('--fullwidth');

    }

  }

  ```

- **Working with ViewChild and local variable (recommended):**

  ```javascript

  import { AfterViewInit, ViewContainerRef, Renderer2 } from '@angular/core';

  export class TableComponent implements AfterViewInit {

    constructor(

      private _vcRef: ViewContainerRef,
      private _renderer: Renderer2

    ) {}

    @ViewChild('myContainer') container : this_vcRef;    

    ngAfterViewInit() {

      this.updateContainer();

    }

    updateContainer() {

      this._renderer.addClass(this.container.nativeElement, '--fullwith');

    }

  }

  ```

**[Back to top](#table-of-contents)**
