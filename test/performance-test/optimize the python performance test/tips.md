# optimize performance test

## Preload related objects
Product.objects.select_related('...')
product.objects.prefetch_related('...')

## Load only what you need
 Product.objects.only('title')
 Product.objects.defer('description')

 ## use values
  Product.objects.values() # we get dict
   Product.objects.valuse_list() we get list

## Count properly
 Product.objects.count()
  len(Product.objects.all())  #BAD

## Bulk create/update(Bulk send one instruction to create or updaTE Mmultiple request) and it is useful when we have multimple create/update request
 Product.objects.bulk_create([])
 
 # Optimizations
 - optimize the python code
 -re-write the query
 - Tune the database
 - Cache the result
 - Buy more hardware
