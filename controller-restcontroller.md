# @Controller vs @RestController:  

* @Controller creates a Map of model object and find a view
* @RestController returns the object and object data is written into HTTP response as JSON or XML.
  * __NOTE__ this can also be done with traditional @Controller and use @ResponseBody annotation but since this is the default behavior of RESTful Web services, Spring introduced @RestController which combined the behavior of @Controller and @ResponseBody together.
* see: [link](https://javarevisited.blogspot.com/2017/08/difference-between-restcontroller-and-controller-annotations-spring-mvc-rest.html)

* Rest mappings: 
  * @GetMapping("/posts/{postId}/comments")
  * @PostMapping("/posts/{postId}/comments")
  * @PutMapping("/posts/{postId}/comments/{commentId}")
  * @DeleteMapping("/posts/{postId}/comments/{commentId}")
