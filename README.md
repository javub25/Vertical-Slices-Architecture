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

We want to specify price product configuration allowed in our application.   
constants folder holds it in one place.

```ts

export const PRODUCT_PRICE = {
  MIN_PRICE: 0,
  ERROR_CODE: 'INVALID_PRICE',
  ERROR_MESSAGE: 'Product price must be zero or greater',
} as const;
```


### 📂 rules/

Contains actions to validate how a Product should be.

Example, ensure a product has a valid price.

```ts
export const isPriceValid = (price: number): boolean => {
  return price >= PRODUCT_PRICE.MIN_PRICE;
}

export const ensurePriceIsValid = (product: Product): ValidationResult => {
  const isValid = isPriceValid(product.price);

   if(isValid)
   {
     return { isValid: true, errors: [] };
   }

   return {
      isValid: false,
      errors: [PRODUCT_PRICE]
  }
};
```       
