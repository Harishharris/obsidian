#### Requirements
1. User can borrow a book
2. User can return a book
3. User will be fined if they return a book late
#### Entities
1. Book
2. BookCopy
3. User
4. Loan
#### Relationships
1. book holds bookcopies
2. user can have bookcopies
3. loan is the trx b/w user and book
#### Responsibilities
1. A book is an entity represents the logical entity of a particular book
2. BookCopy is the physical repr. of the book
3. Loan is the contract b/w user and the book
#### Identify Abstractions
1. maybe fine strategy depending on the book
#### Design principles
#### Design patterns
1. strategy for pricing
#### Flow
1. a user selects a book
2. if we dont have copy of it, we would reject it
3. we would create a loan b/w the user and the bookcopy and attach a period
4. a user would return the book
5. the bookcopy will be back available and the loan is cleared