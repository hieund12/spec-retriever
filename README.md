# spec-retriever
Tự Động Hóa Việc Viết Testcase Từ Tài Liệu Đặt Tả Phần Mềm

### Mục Đích và Lợi Ích:
- Dự án này nhằm mục đích phát triển một hệ thống tự động hoá việc viết testcase từ tài liệu đặt tả của phần mềm, nhằm giảm thiểu sự can thiệp của con người, giảm thời gian phát triển và tăng cường độ chính xác trong quá trình kiểm thử phần mềm. Hệ thống này sẽ giúp các nhà phát triển và kiểm thử viên tập trung vào những vấn đề phức tạp hơn, đồng thời đảm bảo các tiêu chuẩn và yêu cầu kỹ thuật được tuân thủ một cách nghiêm ngặt.

### Các Pha Triển Khai:
#### Thu thập và Chuẩn Bị Dữ Liệu:

- Thu thập tài liệu đặt tả: Sử dụng các tài liệu kỹ thuật, sơ đồ và mô tả tính năng từ các bộ phận kỹ thuật để tạo ra một kho dữ liệu.
- Tiền xử lý: Chuẩn hóa tài liệu để dễ dàng xử lý bằng cách loại bỏ thông tin thừa và định dạng lại văn bản.
- Ví dụ về tài liêu
  - https://www.istqb.org/certifications/certified-tester-foundation-level/
  - https://qawerk.com/blog/website-testing-checklist/
  - https://owasp.org/www-project-top-ten/
  - ...

#### Phương pháp baseline dựa trên BM25
- Tích hợp BM25: Phát triển một công cụ tìm kiếm để xác định và trích xuất các phần tài liệu liên quan dựa trên câu hỏi hoặc từ khóa.
- Xác định ngữ cảnh: Sử dụng các thuật toán để hiểu rõ hơn về ngữ cảnh và ý nghĩa của từng đoạn trong tài liệu.
  - Sử dụng **BERT** và **ChatGPT-4**: Những mô hình này sẽ được sử dụng để phân tích ngữ cảnh và sinh ra các testcase có tính ứng dụng cao dựa trên các thông tin đã được trích xuất.

#### Phương pháp nâng cao sử dụng LLMs
- Word2Vec là một mô hình nhúng từ (word embedding) được phát triển bởi nhóm nghiên cứu của Google. Mô hình này được thiết kế để chuyển đổi các từ thành vector đặc trưng số, sao cho các từ có ngữ nghĩa tương tự nhau sẽ có véc-tơ đặc trưng gần nhau trong không gian vector. Mục đích chính là để máy tính có thể hiểu và xử lý ngôn ngữ tự nhiên một cách hiệu quả hơn, điều này rất có giá trị trong quá trình xử lý và phân tích văn bản lớn.
  -  Trước hết, tài liệu đặt tả sẽ được tiền xử lý, bao gồm việc loại bỏ các từ dư thừa (stop words), chuẩn hóa các từ (lemmatization), và tách từ (tokenization).
  -  Các từ đã được tách ra từ tài liệu đặt tả sẽ được sử dụng để huấn luyện mô hình Word2Vec. Quá trình này bao gồm việc dùng một mạng nơ-ron nhỏ, thường là mạng Skip-gram hoặc CBOW (Continuous Bag of Words), để dự đoán các từ xung quanh từ hiện tại, hoặc ngược lại.
Mỗi từ sẽ được biểu diễn dưới dạng một vector nhiều chiều (thường là 100-300 chiều), với mỗi chiều đại diện cho một đặc trưng ngữ nghĩa của từ đó.
  - Sau khi mô hình Word2Vec đã được huấn luyện, mỗi từ trong tài liệu đặt tả sẽ được chuyển đổi thành vector tương ứng. Điều này cho phép chúng ta biến đổi toàn bộ tài liệu thành một dạng vector.
Các vector từ này có thể được tổng hợp lại để tạo thành vector đại diện cho cả câu, đoạn, hoặc toàn bộ văn bản, thông qua các phương pháp như trung bình cộng, trọng số TF-IDF, hoặc bằng cách sử dụng mạng nơ-ron sâu hơn. 
- Công Nghệ và Công Cụ:
  - **BM25**: Một thuật toán xếp hạng văn bản dựa trên thông tin tìm kiếm, giúp cải thiện khả năng tìm kiếm và liên kết văn bản.
  - **BERT** và **ChatGPT-4**: Những LLMs hiện đại với khả năng hiểu ngữ cảnh vượt trội, hỗ trợ trong việc sinh ra văn bản một cách tự nhiên và đáp ứng nhu cầu cụ thể của dự án.
  - Công nghệ nhúng kiến thức: Sử dụng các mô hình như **Word2Vec**, **GloVe** hoặc **FastText** để chuyển đổi văn bản thành vector, từ đó cải thiện khả năng xử lý ngôn ngữ tự nhiên và trích xuất thông tin.
 
- Khi đã có vector đặc trưng cho các phần của tài liệu, hệ thống có thể sử dụng các kỹ thuật tìm kiếm và so khớp vector để xác định các đoạn văn bản liên quan đến một yêu cầu kiểm thử cụ thể.
- Các đoạn văn bản được xác định này sau đó có thể được dùng để tự động sinh ra testcase bằng cách sử dụng các LLMs như BERT hoặc ChatGPT, với việc tận dụng các đặc trưng ngữ nghĩa đã được nhúng.

#### Kết quả mong đợi
Dự án này không chỉ giảm đáng kể thời gian cần thiết cho quá trình kiểm thử phần mềm mà còn nâng cao độ chính xác và tin cậy của các bài test, qua đó góp phần vào việc phát triển phần mềm hiệu quả và chất lượng cao. 
