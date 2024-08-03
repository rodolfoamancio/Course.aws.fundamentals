# Redesigning the app

Up to this point, the designed app has three layers:
1. Presentation layer: user interface built with `html`, `css` and `js`,
2. Application layer: business and application logic,
3. Data layer: database.

We can change how these layers are hosted and structure, separating the presentation layer from the backend logics. In this case, the presentation layer can be moved to an Amazon `S3` bucket with static website hosting enabled.

Additionally, instead of using EC2, the backend application could be structured in lambda functions, separating each type of request:
1. Create-employee,
2. List-employees,
3. Updates-employees,
4. Delete-employees.

While, database could be stored at Amazon DynamoDB. And the api calls could be handled by Amazon API gateway.
