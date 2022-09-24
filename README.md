# primary_keys_issue
Quite widespread issue of wrong attribution of the same object to different unique identifiers.

Let's consider following:
- We have a food delivery service and we're able to provide it for different restaurants in New York.
- We need couriers for it and there are three possible delivery types: couriers of our service, restaurant's couriers (in case if they have their own delivery) and our partners from some taxi service.
- We have our own sales and support managers. They are able to manage some data related to restaurants manually via web-services and it's a part of some common infrastructure including DWH, BI tools, etc. Let's consider that all ETL processes don't fail and we can fully observe our service.
- Right now we're interested only in such entities as restaurants and its orders.

We found out that one primary key in restaurant's entity means not physically restaurant but the restaurant plus its delivery type: in case if restaurant has its own couriers and we propose our courier service we have to sign two different working agreement with two different legal entities.
Moreover, after some analysis we figure out quite common problem of manually edited systems: the same entities (restaurants in this case) can have a bit different corresponding data.

We need to create the composite primary key of restaurants. In case if we want (sure, we do) to evaluate some statistics regarding restaurants we would not be able to do it due to unexisting of fields with the same values to the same restaurants.

That's quite common issue for different CRM-systems: for example, a customer fills the landing web-page where specifies own name, surname and patronymic. After some time the customer provides this data for another page and doesn't leave patronymic field empty. In this case the customer could be counted twice as two separate users.
