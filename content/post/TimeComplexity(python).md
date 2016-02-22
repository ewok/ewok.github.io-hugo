{
    "date": "2012-12-20",
    "description": null,
    "draft": false,
    "id": 54,
    "image": null,
    "meta_title": null,
    "slug": "timecomplexitypython",
    "tags": [
        "dev"
    ],
    "title": "TimeComplexity(python)",
    "type": "post"
}



Шпаргалка
 
'n' - количество элементов в контейнере
'k' - значение параметра либо количество элементов в параметре
 

    list(Списки):

	Operation | Average Case | Amortized Worst Case
    Copy 	        O(n)				O(n)
    Appednd[1]		O(1)				O(1)
    Insert 			O(n) 				O(n)
    Get item 		O(1) 				O(1)
    Set item 		O(1) 				O(1)
    Delete item 	O(n) 				O(n)
    Iteration 		O(n) 				O(n)
    Get slice 		O(k) 				O(k)
    Delete slice 	O(n) 				O(n)
    Set slice 		O(k + n) 			O(k + n)
    Extend[1] 		O(k) 				O(k)
    Sort 			O(n log n) 			O(n log n)
    Multiply 		O(nk) 				O(nk)
    x in s 			O(n) 	 
    min(s), max(s) 	O(n) 	 
    Get length 		O(1) 				O(1)
 

set(Множества):

    Operation 				Average Case 				Worst Case
    x in s 	 					O(1) 						O(n) 
    Union s|t 					O(len(s) + len(t))  	 
    Intersection s&t  			O(min(len(s), len(t))  		O(len(s) * lent(t)) 
    Difference s-t  			O(len(s))  	 
    s.difference_update(t)  	O(len(t))  	 
    Symmetric Difference s^t  	O(len(s))  				O(len(s) * len(t)) 
    s.symmetric_difference_update(t)  	O(len(t))  		O(len(t) * len(s))

dict(Словари):

    Operation 	Average Case 	Worst Case
    Copy 			O(n) 			O(n)
    Get item 		O(1) 			O(n)
    Set item 		O(1) 			O(n)
    Delete item 	O(1) 			O(n)
    Iteration 		O(n) 			O(n)
 
