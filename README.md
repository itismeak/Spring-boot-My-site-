# Spring-boot-My-site-

**File Handling**
<html xmlns:th="http://www.thymeleaf.org"> - Adding thymleaf properties to HTML
	
1)HTML

    Tips:
    enctype = "multipart/form-data" must define inside a form tag

    <form action ="/upload" method ="post" enctype = "multipart/form-data">
      <input type ="file" name = "files" multiple>
      <input type ="submit" ></input>
      </form>
  
2)controller

    Tips:
     	@RequestParam("files") MultipartFile file
        files -  html/entity present name
        file  - entity reference of MultipartFile class
        transferTo(path) - Move the file source to destination 
	
	model.addAttribute(key,msg) - return a msg to HTML page
	th:text="${msg}" - Receive the controller msg and display HTML Page
        
    @RequestMapping("/upload")
	public String upload(Model model, @RequestParam("files") MultipartFile file) throws IOException {
		String destPath = "D:/file handling/uploads/";
		
		Date date = Calendar.getInstance().getTime();
		DateFormat dateFormat = new SimpleDateFormat("MMM_dd_yyyy hh_mm_ss-");
		String strDate = dateFormat.format(date);

		String destination=destPath + strDate + file.getOriginalFilename();
		String fileName= strDate + file.getOriginalFilename();
		// make a new directory
		boolean destDirectory = new File(destPath).mkdirs();

		// Move a file source to destination
		File moveFile = new File(destination);
		file.transferTo(moveFile);

		// Response msg will display HTML page
		model.addAttribute("msg", "Succesfully uploaded  " + destination);

		return "uploadstatusview";

	}
	
3)HTML Response of file upload

	<div th:if="${msg}">
		<span th:text="${msg}"></span>
	</div>
