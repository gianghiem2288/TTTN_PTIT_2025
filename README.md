# Hướng Dẫn Chương Trình Thực Tập Thiết Kế Phần Cứng
**Thời gian: 20/07/2025 - 20/11/2025**

## Mục Lục
- [Chủ đề 1: Thiết kế CPU với kiến trúc tập lệnh mở RISC-V](#chủ-đề-1-thiết-kế-cpu-với-kiến-trúc-tập-lệnh-mở-risc-v)
  - [Pipeline 3 Stages](#pipeline-3-stages)
  - [Pipeline 4 Stages](#pipeline-4-stages)
  - [Pipeline 5 Stages](#pipeline-5-stages)
- [Chủ đề 2: Thiết kế và Mô hình hóa Bộ điều khiển Bus I2C](#chủ-đề-2-thiết-kế-và-mô-hình-hóa-bộ-điều-khiển-bus-i2c)
- [Chủ đề 3: Thiết kế và Triển khai Bộ xử lý RISC 32-bit](#chủ-đề-3-thiết-kế-và-triển-khai-bộ-xử-lý-risc-32-bit)
- [Chủ đề 4: Bộ điều khiển DMA cho AMBA Bus IP Core](#chủ-đề-4-bộ-điều-khiển-dma-cho-amba-bus-ip-core)
- [Chủ đề 5: Bộ điều khiển SDRAM](#chủ-đề-5-bộ-điều-khiển-sdram)
- [Chủ đề 6: Phát triển giao thức UART, SPI và I2C](#chủ-đề-6-phát-triển-giao-thức-uart-spi-và-i2c)

---

## Chủ đề 1: Thiết kế CPU với kiến trúc tập lệnh mở RISC-V

### Pipeline 3 Stages

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**: 
  - Cơ sở kiến trúc máy tính và tổ chức
  - Đặc tả ISA RISC-V (tập lệnh cơ bản RV32I)
  - Khái niệm thiết kế số cơ bản (mạch tổ hợp và tuần tự)
  - Nguyên lý thiết kế CPU và các thành phần đường dẫn dữ liệu

- **Tuần 3-4**:
  - Kiến trúc pipeline 3 giai đoạn (Fetch, Decode/Execute, Memory/Writeback)
  - Các hazard trong pipeline (dữ liệu, điều khiển, cấu trúc) và giải pháp
  - Phương pháp lập trình HDL (Verilog/VHDL) cho thiết kế CPU
  - Cơ bản về phát triển FPGA

**Kiến thức chuẩn bị:**
- Cơ sở thiết kế số (đại số Boolean, mạch tuần tự)
- Kiến thức cơ bản về kiến trúc máy tính
- Làm quen với ít nhất một ngôn ngữ HDL (ưu tiên Verilog)

**Tài liệu tham khảo:**
- "Computer Organization and Design: The Hardware/Software Interface RISC-V Edition" của D. Patterson và J. Hennessy
- "Digital Design and Computer Architecture: RISC-V Edition" của Sarah Harris và David Harris
- Đặc tả RISC-V: [RISC-V Specifications](https://riscv.org/technical/specifications/)
- "FPGA Prototyping by Verilog Examples" của Pong P. Chu

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- GTKWave để phân tích dạng sóng
- RISC-V GNU Toolchain cho cross-compilation
- Verilator hoặc ModelSim cho mô phỏng RTL

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Thiết kế và triển khai các thành phần pipeline
  - Instruction Fetch (PC, giao diện bộ nhớ lệnh)
  - Decode/Execute (file thanh ghi, ALU, đơn vị điều khiển)
  - Memory/Writeback (giao diện bộ nhớ dữ liệu, logic ghi lại)

- **Tuần 4-6**: Tích hợp pipeline và quản lý hazard
  - Triển khai các thanh ghi pipeline
  - Tín hiệu điều khiển và đường dẫn chuyển tiếp
  - Triển khai dự đoán nhánh (đơn giản)
  - Triển khai giao diện bộ nhớ đệm (nếu áp dụng)

- **Tuần 7-8**: Kiểm thử và xác minh
  - Kiểm tra đơn vị cho từng thành phần
  - Kiểm tra tích hợp cho toàn bộ pipeline
  - Đánh giá hiệu năng
  - Tổng hợp và triển khai FPGA
  
**Sản phẩm:**
- Mã RTL cho bộ xử lý RISC-V 3 giai đoạn
- Test bench và kết quả mô phỏng
- Báo cáo tổng hợp
- Trình diễn CPU hoạt động trên FPGA
- Tài liệu về kiến trúc và các quyết định triển khai

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**: Chuyển đổi RTL sang Gate-Level
  - Cơ bản về tổng hợp logic
  - Các ràng buộc thiết kế và phân tích thời gian
  - Mô phỏng và xác minh ở mức gate

- **Tuần 3-4**: Quy trình physical design
  - Khái niệm floorplanning
  - Kỹ thuật đặt và định tuyến
  - Tổng hợp cây đồng hồ
  - Phân tích và tối ưu hóa công suất
  - Thiết kế cho khả năng kiểm tra (DFT)

**Tài liệu tham khảo bổ sung:**
- "CMOS VLSI Design: A Circuits and Systems Perspective" của Neil Weste và David Harris
- "Static Timing Analysis for Nanometer Designs" của J. Bhasker và Rakesh Chadha
- "ASIC Design in the Silicon Sandbox" của Keith Barr

**Công cụ cho Physical Design:**
- Synopsys Design Compiler hoặc Cadence Genus cho tổng hợp
- Synopsys IC Compiler hoặc Cadence Innovus cho P&R
- Synopsys PrimeTime cho STA
- Cadence Conformal cho kiểm tra tương đương

### Pipeline 4 Stages

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**: 
  - Ôn tập ISA RISC-V (RV32I với các phần mở rộng như M và C)
  - Khái niệm thiết kế số nâng cao
  - Phân cấp bộ nhớ và nguyên tắc thiết kế bộ nhớ đệm
  - Thuật toán số học máy tính

- **Tuần 3-4**:
  - Kiến trúc pipeline 4 giai đoạn (Fetch, Decode, Execute, Memory/Writeback)
  - Phát hiện và giải quyết hazard pipeline nâng cao
  - Kỹ thuật dự đoán nhánh
  - Tối ưu hóa điều khiển pipeline

**Kiến thức chuẩn bị:**
- Kiến thức vững về thiết kế số
- Kiến thức kiến trúc máy tính
- Thành thạo Verilog/VHDL
- Hiểu biết về kiến trúc FPGA

**Tài liệu tham khảo:**
- Giống như pipeline 3 giai đoạn, thêm:
- "Parallel Computer Architecture: A Hardware/Software Approach" của David Culler và cộng sự
- "Modern Processor Design: Fundamentals of Superscalar Processors" của John Shen và Mikko Lipasti
- Các bài báo nghiên cứu về tối ưu hóa pipeline

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Thiết kế và triển khai các giai đoạn pipeline
  - Giai đoạn Instruction Fetch
  - Giai đoạn Instruction Decode
  - Giai đoạn Execute với ALU
  - Giai đoạn Memory/Writeback

- **Tuần 4-6**: Tích hợp pipeline và tính năng nâng cao
  - Triển khai đơn vị điều khiển pipeline
  - Thiết kế logic chuyển tiếp
  - Đơn vị dự đoán nhánh
  - Tích hợp bộ nhớ đệm
  - Triển khai bộ đếm hiệu suất

- **Tuần 7-8**: Kiểm thử, xác minh và tối ưu hóa
  - Phát triển bộ kiểm thử toàn diện
  - Tối ưu hóa thời gian
  - Tối ưu hóa diện tích
  - Phân tích và tối ưu hóa công suất
  - Triển khai và xác minh trên FPGA

**Sản phẩm:**
- Mã RTL cho bộ xử lý RISC-V 4 giai đoạn
- Test bench toàn diện
- Báo cáo tổng hợp và phân tích thời gian
- Trình diễn FPGA với các số liệu hiệu suất
- Tài liệu kỹ thuật với chi tiết kiến trúc

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**: Quy trình RTL-to-GDSII nâng cao
  - Phương pháp thiết kế phân cấp
  - Phân tích multi-corner multi-mode (MCMM)
  - Khái niệm phân tích thời gian tĩnh
  - Kỹ thuật thiết kế công suất thấp

- **Tuần 3-4**: Xác minh vật lý và signoff
  - Kiểm tra quy tắc thiết kế (DRC)
  - Layout versus schematic (LVS)
  - Trích xuất ký sinh
  - Mô phỏng sau layout
  - Phân tích IR drop và EM

**Tài liệu tham khảo bổ sung:**
- "Low Power Design Essentials" của Jan Rabaey
- "Logical Effort: Designing Fast CMOS Circuits" của Sutherland, Sproull và Harris
- Các bài báo nghiên cứu về phương pháp physical design hiện đại

### Pipeline 5 Stages

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**: 
  - Nghiên cứu toàn diện về ISA RISC-V (bao gồm phần mở rộng F, D)
  - Nguyên tắc vi kiến trúc nâng cao
  - Khái niệm thực thi ngoài thứ tự
  - Nguyên tắc kiến trúc siêu vô hướng

- **Tuần 3-4**:
  - Kiến trúc pipeline 5 giai đoạn (Fetch, Decode, Execute, Memory, Writeback)
  - Dự đoán nhánh nâng cao và thực thi đoán trước
  - Xử lý ngoại lệ và ngắt chính xác
  - Phương pháp phân tích hiệu suất

**Kiến thức chuẩn bị:**
- Kiến thức thiết kế số nâng cao
- Kiến thức vững chắc về kiến trúc máy tính
- Kỹ năng lập trình HDL nâng cao
- Hiểu biết về các khái niệm thời gian nâng cao

**Tài liệu tham khảo:**
- Tất cả tài liệu tham khảo từ pipeline 3 và 4 giai đoạn, cộng thêm:
- "Computer Architecture: A Quantitative Approach" của J. Hennessy và D. Patterson
- "Synthesis and Optimization of Digital Circuits" của Giovanni De Micheli
- "High-Performance Embedded Computing" của Wayne Wolf

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Thiết kế chi tiết các giai đoạn pipeline
  - Instruction Fetch với dự đoán nhánh nâng cao
  - Instruction Decode với đổi tên thanh ghi
  - Execute stage với các đơn vị thực thi phức tạp
  - Memory stage với giao diện bộ nhớ đệm
  - Writeback stage với chuyển tiếp kết quả

- **Tuần 4-6**: Triển khai tính năng nâng cao
  - Cơ chế xử lý ngoại lệ
  - Tích hợp đơn vị quản lý bộ nhớ (MMU)
  - Triển khai giao thức nhất quán bộ nhớ đệm
  - Cơ chế chuyển tiếp nâng cao
  - Các đơn vị giám sát hiệu suất

- **Tuần 7-8**: Kiểm thử toàn diện và tối ưu hóa
  - Phương pháp kiểm thử nâng cao (UVM/OVM)
  - Đánh giá hiệu suất với các bộ benchmark tiêu chuẩn
  - Kỹ thuật tối ưu hóa diện tích và công suất
  - Phương pháp đóng thời gian
  - Triển khai FPGA với cơ sở hạ tầng gỡ lỗi

**Sản phẩm:**
- Mã RTL cho bộ xử lý RISC-V 5 giai đoạn
- Môi trường kiểm thử nâng cao (dựa trên UVM/OVM)
- Báo cáo tổng hợp và phân tích thời gian đầy đủ
- Trình diễn FPGA với kết quả benchmark
- Tài liệu kỹ thuật với chi tiết kiến trúc và triển khai

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**: Quy trình physical design nâng cao
  - Kỹ thuật floorplanning phân cấp
  - Phân tích clock domain crossing (CDC)
  - Kỹ thuật tối ưu hóa công suất nâng cao
  - Tích hợp trình biên dịch bộ nhớ

- **Tuần 3-4**: Xác minh vật lý và chuẩn bị tapeout
  - Kỹ thuật DRC và LVS nâng cao
  - Phân tích toàn vẹn tín hiệu
  - Phân tích electromigration và IR drop
  - Quy trình xác minh cuối cùng và signoff

**Tài liệu tham khảo bổ sung:**
- "Advanced ASIC Chip Synthesis" của Himanshu Bhatnagar
- "Static Timing Analysis for Nanometer Designs" của J. Bhasker và Rakesh Chadha
- Các bài báo nghiên cứu về kỹ thuật physical design nâng cao cho bộ xử lý hiện đại

---

## Chủ đề 2: Thiết kế và Mô hình hóa Bộ điều khiển Bus I2C

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**:
  - Cơ bản về giao thức I2C (chế độ tiêu chuẩn, nhanh, nhanh+, tốc độ cao)
  - Đặc tính điện và đặc điểm thời gian của bus I2C
  - Nguyên tắc truyền thông nối tiếp
  - Phương pháp thiết kế máy trạng thái

- **Tuần 3-4**:
  - Kiến trúc master và slave I2C
  - Cơ chế kéo dài xung đồng hồ và trọng tài
  - Nhận dạng địa chỉ và giao thức truyền
  - Cơ chế phát hiện lỗi và phục hồi

**Kiến thức chuẩn bị:**
- Cơ bản về thiết kế số
- Khái niệm máy trạng thái
- Kiến thức cơ bản về giao thức truyền thông nối tiếp
- Kỹ năng lập trình HDL (Verilog/VHDL)

**Tài liệu tham khảo:**
- "I2C Bus Specification and User Manual" của NXP Semiconductors
- "Digital Design with RTL Design, Verilog and VHDL" của Frank Vahid
- "FPGA Prototyping by Verilog Examples" của Pong P. Chu
- "The I2C Bus: From Theory to Practice" của Dominique Paret

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- ModelSim hoặc tương tự cho mô phỏng HDL
- Logic analyzer (phần cứng hoặc phần mềm)
- Bộ phân tích giao thức I2C (tùy chọn)

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Thiết kế bộ điều khiển I2C cơ bản
  - Đơn vị tạo xung đồng hồ
  - Máy trạng thái điều khiển mức bit
  - Triển khai thanh ghi dịch
  - Tạo START, STOP và ACK/NACK

- **Tuần 4-6**: Giao diện và tính năng nâng cao
  - Giao diện APB/AXI slave cho cấu hình thanh ghi
  - Hỗ trợ đa master với trọng tài
  - Giao diện DMA cho thông lượng cao hơn
  - Triển khai FIFO cho bộ đệm TX/RX

- **Tuần 7-8**: Kiểm thử và xác minh
  - Kiểm tra tuân thủ giao thức ở mức bit
  - Giao diện với các thiết bị ngoại vi I2C tiêu chuẩn
  - Xác minh thời gian theo đặc tả
  - Triển khai FPGA và kiểm thử thực tế

**Sản phẩm:**
- Mã RTL cho bộ điều khiển I2C (khả năng master và slave)
- Test bench toàn diện với các kiểm tra tuân thủ giao thức
- Báo cáo tổng hợp và phân tích thời gian
- Trình diễn FPGA với các thiết bị ngoại vi I2C thực
- Tài liệu kỹ thuật

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**:
  - Tối ưu hóa tổng hợp logic cho giao diện nối tiếp
  - Vấn đề và giải pháp clock domain crossing
  - Lựa chọn và cấu hình I/O pad
  - Phân tích toàn vẹn tín hiệu cho tín hiệu I2C

- **Tuần 3-4**:
  - Các cân nhắc triển khai vật lý
  - Kiểm tra và xác minh ở mức vật lý
  - Chèn scan chain
  - Đặc tính và mô hình hóa I/O

**Tài liệu tham khảo bổ sung:**
- "Skew-Tolerant Circuit Design" của David Harris
- Các ghi chú ứng dụng về triển khai I2C từ NXP, TI, v.v.
- "Design for Testability" của Charles E. Stroud

---

## Chủ đề 3: Thiết kế và Triển khai Bộ xử lý RISC 32-bit

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**:
  - Nguyên tắc và lịch sử kiến trúc RISC
  - Thiết kế kiến trúc tập lệnh
  - Phương pháp thiết kế đường dẫn dữ liệu và đơn vị điều khiển
  - Cơ bản về phân cấp bộ nhớ

- **Tuần 3-4**:
  - Nguyên tắc kiến trúc pipeline
  - Phát hiện và xử lý hazard
  - Thiết kế bộ thanh ghi
  - Thiết kế ALU cho các phép toán 32-bit
  - Giao diện bộ nhớ lệnh và dữ liệu

**Kiến thức chuẩn bị:**
- Cơ bản về thiết kế số
- Khái niệm kiến trúc máy tính
- Kỹ năng lập trình HDL
- Đại số Boolean và logic tuần tự

**Tài liệu tham khảo:**
- "Computer Organization and Design: The Hardware/Software Interface" của D. Patterson và J. Hennessy
- "Digital Design and Computer Architecture" của David Harris và Sarah Harris
- "MIPS RISC Architecture" của G. Kane và J. Heinrich (tham khảo cho kiến trúc RISC cổ điển)
- "Microprocessor Design: A Practical Guide from Design Planning to Manufacturing" của Grant McFarland

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- ModelSim hoặc tương tự cho mô phỏng HDL
- GNU GCC/Binutils cho cross-compilation (nếu triển khai ISA tùy chỉnh)
- Architectural simulator (tùy chọn, ví dụ: SimpleScalar)

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Triển khai các thành phần cốt lõi
  - Triển khai bộ giải mã lệnh
  - Bộ thanh ghi với hai cổng đọc
  - ALU với các phép toán 32-bit đầy đủ
  - Bộ đếm chương trình và logic nhánh
  - Bộ điều khiển giao diện bộ nhớ

- **Tuần 4-6**: Tích hợp pipeline và tính năng
  - Tích hợp các giai đoạn pipeline
  - Đơn vị phát hiện hazard
  - Đường dẫn chuyển tiếp dữ liệu
  - Triển khai đơn vị điều khiển
  - Logic xử lý ngoại lệ

- **Tuần 7-8**: Kiểm thử và tối ưu hóa
  - Kiểm tra bộ lệnh
  - Phân tích hiệu suất pipeline
  - Triển khai dự đoán nhánh
  - Tổng hợp và tối ưu hóa thời gian
  - Triển khai và xác minh trên FPGA

**Sản phẩm:**
- Mã RTL đầy đủ cho bộ xử lý RISC 32-bit
- Bộ công cụ assembler hoặc compiler (cơ bản)
- Các chương trình kiểm tra chức năng
- Báo cáo tổng hợp và hiệu suất
- Trình diễn bộ xử lý hoạt động trên FPGA
- Tài liệu kỹ thuật và hướng dẫn lập trình

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**:
  - Chiến lược floorplanning cho thiết kế bộ xử lý
  - Thiết kế mạng phân phối đồng hồ
  - Phân tích và tối ưu hóa công suất
  - Phân tích và tối ưu hóa đường tới hạn

- **Tuần 3-4**:
  - Kỹ thuật tối ưu hóa đặt và định tuyến
  - Chèn scan chain và DFT
  - Phương pháp phân tích thời gian tĩnh
  - Xác minh vật lý và sign-off

**Tài liệu tham khảo bổ sung:**
- "CMOS VLSI Design: A Circuits and Systems Perspective" của Neil Weste và David Harris
- "Principles of CMOS VLSI Design" của Neil Weste và Kamran Eshraghian
- "The Designer's Guide to VHDL" hoặc "RTL Hardware Design Using VHDL" cho tham khảo triển khai

---

## Chủ đề 4: Bộ điều khiển DMA cho AMBA Bus IP Core

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**:
  - Kiến trúc và đặc tả bus AMBA (AHB, AXI, APB)
  - Cơ bản về bộ điều khiển DMA và các chế độ hoạt động
  - Kỹ thuật ánh xạ bộ nhớ và giải mã địa chỉ
  - Cơ chế trọng tài bus

- **Tuần 3-4**:
  - Tính năng DMA nâng cao (scatter-gather, buffer vòng)
  - Cơ chế xử lý ngắt và ưu tiên
  - Kỹ thuật quản lý buffer
  - Chiến lược tối ưu hóa hiệu suất cho giao dịch bus

**Kiến thức chuẩn bị:**
- Cơ bản về thiết kế số
- Hiểu biết về giao thức bus
- Kiến thức về kiến trúc hệ thống bộ nhớ
- Kinh nghiệm lập trình HDL

**Tài liệu tham khảo:**
- "AMBA AXI and ACE Protocol Specification" của ARM
- "AMBA AHB and APB Protocol Specification" của ARM
- "System-on-Chip Design with Arm® Cortex®-M Processors" của Joseph Yiu
- "Embedded SoPC Design with Nios II Processor and VHDL Examples" của Pong P. Chu

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- ModelSim cho mô phỏng
- AMBA Verification IP (VIP) nếu có
- Logic analyzer cho xác minh giao thức

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Triển khai bộ DMA cốt lõi
  - Thiết kế bộ điều khiển kênh
  - Đơn vị tạo địa chỉ
  - Logic kiểm soát kích thước truyền
  - Bộ đệm FIFO cho staging dữ liệu
  - Bộ điều khiển giao dịch burst

- **Tuần 4-6**: Giao diện bus và tính năng nâng cao
  - Triển khai giao diện master AXI/AHB
  - Giao diện slave APB để truy cập thanh ghi
  - Xử lý mô tả scatter-gather
  - Tích hợp bộ điều khiển ngắt
  - Trọng tài dựa trên ưu tiên

- **Tuần 7-8**: Xác minh và tích hợp hệ thống
  - Xác minh tuân thủ giao thức
  - Đánh giá hiệu suất
  - Tích hợp hệ thống với bộ nhớ và ngoại vi
  - Thiết lập trình diễn FPGA
  - Kiểm tra trường hợp biên và khôi phục lỗi

**Sản phẩm:**
- Mã RTL cho bộ điều khiển DMA với giao diện AMBA
- Test bench với các kiểm tra giao dịch toàn diện
- Ví dụ tích hợp hệ thống
- Báo cáo phân tích hiệu suất
- Trình diễn FPGA với thông lượng đo được
- Tài liệu kỹ thuật và hướng dẫn lập trình

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**:
  - Hướng dẫn triển khai vật lý đặc thù cho bus AMBA
  - Kỹ thuật đóng timing cho bus tốc độ cao
  - Xử lý clock domain crossing
  - Kỹ thuật thiết kế công suất thấp cho hoạt động DMA

- **Tuần 3-4**:
  - Xác minh vật lý cho giao diện bus
  - Kỹ thuật tối ưu hóa diện tích
  - Các cân nhắc DFT cho bộ điều khiển phức tạp
  - Xác minh thiết kế vật lý cuối cùng

**Tài liệu tham khảo bổ sung:**
- "System Design with SystemC" của Thorsten Grötker và các cộng sự
- "Verification Methodology Manual for SystemVerilog" của ARM và Synopsys
- Các white paper của ARM về hướng dẫn triển khai AMBA

---

## Chủ đề 5: Bộ điều khiển SDRAM

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1-2**:
  - Kiến trúc và nguyên lý hoạt động SDRAM
  - Tham số thời gian và ràng buộc của SDRAM
  - Cơ bản về bộ điều khiển bộ nhớ
  - Cơ chế và yêu cầu làm tươi

- **Tuần 3-4**:
  - Thuật toán lập lịch lệnh
  - Chiến lược quản lý bank
  - Hoạt động burst và chế độ truyền dữ liệu
  - Kỹ thuật ánh xạ địa chỉ
  - Tính năng quản lý năng lượng (self-refresh, power-down)

**Kiến thức chuẩn bị:**
- Cơ bản về thiết kế số
- Kiến thức về mạch số đồng bộ
- Thiết kế máy trạng thái
- Khái niệm kiến trúc hệ thống bộ nhớ

**Tài liệu tham khảo:**
- Đặc tả SDRAM của JEDEC (ví dụ: DDR, DDR2, DDR3)
- "Memory Systems: Cache, DRAM, Disk" của Bruce Jacob và các cộng sự
- "FPGA-Based System Design" của Wayne Wolf
- "Digital Systems Design with FPGAs and CPLDs" của Ian Grout
- Bảng dữ liệu SDRAM từ các nhà sản xuất (Micron, Samsung, v.v.)

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- ModelSim cho mô phỏng
- Memory controller verification IP (nếu có)
- Công cụ phân tích thời gian
- Mô hình SDRAM cho mô phỏng

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-3**: Các thành phần điều khiển cốt lõi
  - Máy trạng thái lệnh
  - Bộ đếm và điều khiển làm tươi
  - Logic ánh xạ địa chỉ
  - Thiết kế đường dẫn dữ liệu (đường đọc/ghi)
  - Bộ điều khiển trình tự khởi tạo

- **Tuần 4-6**: Tính năng nâng cao và tối ưu hóa
  - Logic quản lý bank
  - Sắp xếp lại lệnh để tăng hiệu quả
  - Đọc/ghi cân bằng (cho DDR3/4)
  - Logic tự động precharge
  - Tích hợp quản lý năng lượng
  - Logic clock domain crossing

- **Tuần 7-8**: Xác minh và tích hợp hệ thống
  - Xác minh thời gian theo đặc tả JEDEC
  - Đánh giá hiệu suất
  - Tích hợp giao diện bus (AXI/AHB)
  - Triển khai FPGA với SDRAM thực
  - Cơ chế phát hiện và xử lý lỗi

**Sản phẩm:**
- Mã RTL cho bộ điều khiển SDRAM
- Tham số có thể cấu hình cho các loại SDRAM khác nhau
- Test bench toàn diện với kiểm tra thời gian
- Báo cáo tổng hợp và phân tích thời gian
- Trình diễn FPGA với SDRAM thực
- Báo cáo phân tích hiệu suất (băng thông, độ trễ)
- Tài liệu kỹ thuật và hướng dẫn tích hợp

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**:
  - Ràng buộc thời gian I/O cho giao diện bộ nhớ
  - Thiết kế DLL/PLL cho căn chỉnh đồng hồ
  - Phân tích toàn vẹn tín hiệu cho giao diện tốc độ cao
  - Kỹ thuật kết hợp trở kháng và kết thúc

- **Tuần 3-4**:
  - Các cân nhắc layout cho bộ điều khiển bộ nhớ
  - Xác minh vật lý cho giao diện tốc độ cao
  - DFT cho giao diện bộ nhớ
  - Các cân nhắc cấp board cho giao diện SDRAM

**Tài liệu tham khảo bổ sung:**
- "High-Speed Digital Design: A Handbook of Black Magic" của Howard Johnson và Martin Graham
- Ghi chú ứng dụng từ Micron, Samsung về thiết kế giao diện SDRAM
- "Signal and Power Integrity - Simplified" của Eric Bogatin

---

## Chủ đề 6: Phát triển giao thức UART, SPI và I2C

#### Tháng 1: Nghiên cứu Lý thuyết (20/07 - 20/08/2025)
- **Tuần 1**:
  - Đặc tả giao thức UART và cơ bản
  - Kỹ thuật tạo tốc độ baud
  - Nguyên tắc truyền thông bất đồng bộ
  - Cơ chế phát hiện lỗi (parity, framing)

- **Tuần 2**:
  - Đặc tả giao thức SPI và các chế độ
  - Kiến trúc truyền thông song công đầy đủ
  - Cấu hình đa slave
  - Cấu hình cực và pha đồng hồ

- **Tuần 3**:
  - Đặc tả giao thức I2C và chế độ địa chỉ
  - Triển khai open-drain/open-collector
  - Cơ chế kéo dài đồng hồ và trọng tài
  - Kỹ thuật địa chỉ nâng cao

- **Tuần 4**:
  - Phân tích so sánh ba giao thức
  - Kỹ thuật chuyển đổi giao thức
  - Thiết kế hệ thống đa giao thức
  - Triển khai dựa trên ngắt so với polling

**Kiến thức chuẩn bị:**
- Cơ bản về thiết kế số
- Thiết kế máy trạng thái
- Cơ bản về truyền thông nối tiếp
- Kinh nghiệm lập trình HDL

**Tài liệu tham khảo:**
- "Serial Port Complete" của Jan Axelson
- Đặc tả I2C của NXP Semiconductors
- SPI Block Guide của Motorola/Freescale
- "UART: A Hardware Communication Protocol" (các ghi chú ứng dụng khác nhau)
- "FPGA Prototyping By Verilog Examples" của Pong P. Chu
- Ghi chú ứng dụng từ TI, Microchip, NXP về giao diện nối tiếp

**Công cụ cần thiết:**
- Xilinx Vivado Design Suite hoặc Intel Quartus Prime
- ModelSim cho mô phỏng
- Logic analyzer (phần cứng hoặc phần mềm)
- Bộ phân tích giao thức cho UART, SPI, I2C
- Oscilloscope để xác minh tín hiệu

#### Tháng 2-3: Giai đoạn Triển khai (21/08 - 20/10/2025)
- **Tuần 1-2**: Triển khai UART
  - Mô-đun truyền và nhận
  - Bộ tạo tốc độ baud
  - Tích hợp FIFO
  - Triển khai điều khiển luồng (RTS/CTS)
  - Phát hiện và xử lý lỗi

- **Tuần 3-4**: Triển khai SPI
  - Mô-đun master và slave
  - Bộ tạo đồng hồ với cấu hình cực/pha
  - Xử lý lựa chọn đa slave
  - Mở rộng SPI kép và bốn kênh (nếu áp dụng)
  - Tích hợp FIFO

- **Tuần 5-6**: Triển khai I2C
  - Máy trạng thái master và slave
  - Tạo và đồng bộ hóa đồng hồ
  - Logic nhận diện địa chỉ
  - Trọng tài đa master
  - Hỗ trợ kéo dài đồng hồ

- **Tuần 7-8**: Tích hợp và xác minh
  - Thiết kế giao diện bus chung cho tất cả các giao thức
  - Cơ chế chuyển đổi giao thức
  - Tích hợp với bộ xử lý
  - Kiểm tra toàn diện với thiết bị thực
  - Xác minh hiệu suất và tuân thủ

**Sản phẩm:**
- Mã RTL cho các bộ điều khiển UART, SPI và I2C
- Thiết kế giao diện thanh ghi chung
- Test bench toàn diện cho mỗi giao thức
- Báo cáo tổng hợp và phân tích thời gian
- Trình diễn FPGA với các thiết bị ngoại vi
- Dấu vết từ bộ phân tích giao thức cho thấy sự tuân thủ
- Tài liệu kỹ thuật và hướng dẫn lập trình

#### Tháng 4: Nghiên cứu Physical Design (21/10 - 20/11/2025)
- **Tuần 1-2**:
  - Lựa chọn tiêu chuẩn I/O cho các giao thức khác nhau
  - Ràng buộc thời gian cho giao diện nối tiếp
  - Kỹ thuật clock domain crossing
  - Vấn đề chuyển mức điện áp và tương thích

- **Tuần 3-4**:
  - Các cân nhắc thiết kế vật lý cho giao diện tín hiệu hỗn hợp
  - Các cân nhắc EMI/EMC cho giao diện nối tiếp
  - DFT cho giao diện nối tiếp
  - Kỹ thuật công suất thấp cho bộ điều khiển nối tiếp

**Tài liệu tham khảo bổ sung:**
- "High-Speed Digital Design" của Howard Johnson
- "Signal Integrity Issues and Printed Circuit Board Design" của Douglas Brooks
- Ghi chú ứng dụng về triển khai vật lý giao diện nối tiếp từ các nhà sản xuất bán dẫn

## Hướng Dẫn Chung

### Tiêu Chuẩn Tài Liệu
- Báo cáo tiến độ hàng tuần
- Ghi lại tất cả các quyết định thiết kế với lý do
- Cung cấp chú thích đầy đủ trong mã
- Tạo hướng dẫn sử dụng cho các triển khai cuối cùng

### Mốc Đánh Giá
- Cuối tháng 1: Đánh giá Nghiên cứu Lý thuyết
- Giữa tháng 3: Đánh giá Tiến độ Triển khai
- Cuối tháng 3: Trình diễn MVP
- Cuối tháng 4: Hoàn tất Dự án và Báo cáo

### Định Dạng Sản Phẩm
- Mã nguồn trong kho Git
- Tài liệu ở định dạng Markdown và PDF
- Slide thuyết trình ở định dạng PDF
- Video trình diễn triển khai hoạt động
- Kết quả kiểm thử với tiêu chí đạt/không rõ ràng

### Quy Trình Phát Triển
1. Phân tích yêu cầu và đặc tả
2. Thiết kế kiến trúc và tài liệu
3. Thiết kế cấp mô-đun
4. Triển khai và kiểm thử đơn vị
5. Tích hợp và kiểm thử hệ thống
6. Tối ưu hóa hiệu suất
7. Hoàn thiện báo cáo
