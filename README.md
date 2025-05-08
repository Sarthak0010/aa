#aa

if(empty(items('Apply_to_each_2')?['Date Start']), '', concat(items('Apply_to_each_2')?['Date Start'], 'T09:00:00'))
if(empty(items('Apply_to_each_2')?['Date End']), '', concat(items('Apply_to_each_2')?['Date End'], 'T18:00:00'))
