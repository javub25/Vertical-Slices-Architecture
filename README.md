# Vertical-Slices-Architecture
Clean Frontend Archuitecture - Vertical Slices


## 📗 📂 Domain Layer

Contains business rules that the application must follow.  
Those rules won't changed across application.  
**No React, Angular or database code allowed.**

```css
src/
└── features/
    ├── products/
         ├── domain/
           ├── models/
           |  └── Product.models.ts
           ├── constants/
           |  └── Product.constants.ts
           ├── rules/
              └── Product.rules.ts
```
Architecture with products feature.  

### 📂 models/

Defines data shape names such as:
  - TypeScript **(interfaces, types)**.
  - JavaScript **classes with their own methods**.

```ts
export type ProductId = string;

export interface Product {
  id: ProductId;     
  name: string;
  description: string;
  price: number;       
}
```

### 📂 constants

We want to specify 4 Product Categories allowed in our application. 
Only them.    
constants folder holds those categories.

```ts

export const PRODUCT_CATEGORIES = ['Electronics', 'Food', 'Clothing', 'Services'];
```


### 📂 rules/

Contains actions to validate how a Product should be.

Example, make sure a product belongs to an **authorized** category.

```ts
export const isCategoryValid = (product: Product): boolean => {
  return PRODUCT_CATEGORIES.includes(product.category);
};
```        
