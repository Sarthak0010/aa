#aa

if(
  empty(items('Apply_to_each')?['Date End']),
  '',
  concat(
    formatDateTime(
      parseDateTime(items('Apply_to_each')?['Date End'], 'dd-MM-yyyy'),
      'yyyy-MM-dd'
    ),
    'T18:00:00'
  )
)
