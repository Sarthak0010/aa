#aa

if(
  empty(items('Apply_to_each')?['Date Start']),
  '',
  concat(
    formatDateTime(
      parseDateTime(items('Apply_to_each')?['Date Start'], 'dd-MM-yyyy'),
      'yyyy-MM-dd'
    ),
    'T09:00:00'
  )
)
