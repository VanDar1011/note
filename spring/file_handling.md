# Học cách uploadFile

```sh
@PostMapping(value = "/upload", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
public String fileUpload(@RequestParam("file") MultipartFile file) {
   return null;
}
```

bị cros : thêm vào hàm chỗ chương trình chính

```sh
//    @Bean
//    public WebMvcConfigurer corsConfigurer() {
//        return new WebMvcConfigurer() {
//            @Override
//            public void addCorsMappings(CorsRegistry registry) {
//               registry.addMapping("/**").allowedOrigins("*").allowedMethods("*");
//            }
//        };
//    }
```

## Viết phương thức để gửi file về server, tải file từ server về thành công

```sh
package interceptor.controller;

import interceptor.model.Response;
import org.springframework.core.io.InputStreamResource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

@RestController
@RequestMapping(path = "api/v1")
//@CrossOrigin(origins = "http://127.0.0.1:5500/")
public class UploadFileController {
    @PostMapping(value = "/upload", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public ResponseEntity<Response> fileUpload(@RequestParam("file") MultipartFile file) throws IOException {
        File uploadDir = new File("./uploads");  // Use your desired directory (absolute or relative
        // path)

        // Create the directory if it doesn't exist
        if (!uploadDir.exists()) {
            uploadDir.mkdirs();
        }

        // Define the file path where the image will be saved
        File convertFile = new File(uploadDir, file.getOriginalFilename());

        // Create a new file on the disk and write the uploaded image to that file
        convertFile.createNewFile();

        try (FileOutputStream fout = new FileOutputStream(convertFile)) {
            fout.write(file.getBytes());
        }

        System.out.println("Image is uploaded successfully");

        return ResponseEntity.status(HttpStatus.OK).body(new Response("Image uploaded successfully"));
    }
    @GetMapping(value = "/download")
    public ResponseEntity<Object> downloadFile() throws IOException {
        String filename = "./uploads/a.png";
        File file = new File(filename);
        InputStreamResource resource = new InputStreamResource(new FileInputStream(file));
        HttpHeaders headers = new HttpHeaders();

        headers.add("Content-Disposition", String.format("attachment; filename=\"%s\"", file.getName()));
        headers.add("Cache-Control", "no-cache, no-store, must-revalidate");
        headers.add("Pragma", "no-cache");
        headers.add("Expires", "0");

        ResponseEntity<Object>
                responseEntity = ResponseEntity.ok().headers(headers).contentLength(
                file.length()).contentType(MediaType.parseMediaType("application/txt")).body(resource);

        return responseEntity;
    }
}
```
