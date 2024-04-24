## 1 component.h
File này định nghĩa một lớp trừu tượng tên là "Component" và định nghĩa một số phương thức ảo mà mọi lớp con của nó cần phải triển khai. Cụ thể:

- Phương thức prepare(): Được gọi trước khi các tín hiệu đầu vào được gửi vào mạng: có thể được sử dụng để chuẩn bị thành phần để nhận các tín hiệu trước khi thực thi.
- Phương thức run(): Được gọi sau khi các tín hiệu đầu vào được gửi vào mạng: thực hiện tất cả các xử lý cần thiết cho tick hiện tại.
- Phương thức receivePacket(Packet packet): Được gọi mỗi khi bộ định tuyến nhận một gói tin dành cho thành phần này.
Ngoài ra, file cũng khai báo một số biến dùng chung như con trỏ tới một đối tượng Router, và các biến x và y để định vị vị trí của thành phần trong mạng.

## 2 Config.hpp
- Khai báo thư viện và enum: Đầu tiên, file này bắt đầu với các khai báo thư viện và định nghĩa các enum. Các enum được sử dụng để định nghĩa các tùy chọn và hằng số cho cấu hình.
- Lớp ConfigDecodingException: Đây là một lớp ngoại lệ được sử dụng để xử lý các ngoại lệ phát sinh trong quá trình giải mã cấu hình từ tệp JSON.
- Lớp Config: Lớp này chứa các phương thức và biến tĩnh để xử lý cấu hình. Các phương thức bao gồm:
- - setParameters(): Được sử dụng để đọc cấu hình từ tệp JSON và lưu trữ vào một biến static của lớp.
- - validateParameters(): Kiểm tra tính hợp lệ của cấu hình bằng cách kiểm tra giới hạn và định dạng của các tham số cấu hình.
- - Các phương thức khác để kiểm tra và truy xuất cấu hình đã đọc.

Tóm lại, file "config.hpp" đóng vai trò quan trọng trong việc quản lý cấu hình cho ứng dụng và cung cấp các công cụ để đọc, kiểm tra và truy xuất các thông tin cấu hình từ tệp JSON.

## 3 core.cpp
Đoạn mã trong file "core.cpp" định nghĩa các phương thức của lớp Core, đại diện cho một nhân tố cơ bản trong hệ thống xử lý cấu trúc mạng. Dưới đây là tóm tắt hoạt động của các phương thức trong đoạn mã:

- Constructor:
Có các constructor khác nhau cho việc tạo đối tượng Core. Mỗi constructor khởi tạo các thành viên của lớp Core bằng cách tạo ra các đối tượng Router, Scheduler, NeuronBlock, và CoreController.
Các tham số truyền vào constructor cho phép xác định các core lân cận, bộ nhớ CSRAM, neuron_instructions, vị trí của core, loại và giá trị reset của neuron.

- Phương thức to_string():
Trả về một chuỗi mô tả vị trí của core trong lưới.
- Phương thức prepare():
Gọi phương thức updateCurrentWord() của Scheduler để cập nhật từ hiện tại.
- Phương thức run():
Gọi phương thức run() của CoreController để thực thi logic xử lý của core.
- Phương thức receivePacket(Packet packet):
Gọi phương thức receivePacket(Packet packet) của Scheduler để xử lý gói tin được nhận.

Tóm lại, đoạn mã này thực hiện việc khởi tạo và quản lý các thành phần chính của một core trong hệ thống xử lý cấu trúc lưới, bao gồm định nghĩa các phương thức để chuẩn bị, thực thi và xử lý các gói tin.

## 4 core.h
Đoạn mã trong file "core.h" định nghĩa lớp Core, đại diện cho một nhân tố cơ bản trong hệ thống xử lý cấu trúc mạng. Dưới đây là tóm tắt hoạt động của mã:

- Định nghĩa lớp Core: Lớp Core được kế thừa từ lớp Component, đảm bảo rằng các đối tượng Core có các phương thức cơ bản như prepare(), run(), và receivePacket(Packet packet).
- Các constructors: Có nhiều phiên bản constructor cho phép tạo đối tượng Core với các cấu hình khác nhau. Các tham số của các constructors này cho phép xác định các core lân cận, bộ nhớ CSRAM, hướng dẫn neuron, vị trí của core, loại và giá trị reset của neuron.
- Phương thức prepare(): Được kế thừa từ lớp Component, phương thức này được gọi để chuẩn bị core trước khi chạy.
- Phương thức run(): Được kế thừa từ lớp Component, phương thức này chạy logic xử lý của core.
- Phương thức receivePacket(Packet packet): Được kế thừa từ lớp Component, phương thức này được gọi khi core nhận được một gói tin.
- Phương thức to_string(): Trả về một chuỗi mô tả vị trí của core trong lưới.
- Các thành phần của Core: Scheduler, NeuronBlock, và CoreController là các thành phần chính của một core trong hệ thống xử lý cấu trúc lưới.

## 5 corecontroller.cpp
Đoạn mã trong tệp "corecontroller.cpp" triển khai các phương thức của lớp CoreController, là một thành phần quan trọng của mỗi nhân tố cơ bản trong hệ thống xử lý cấu trúc mạng. Dưới đây là tóm tắt hoạt động của mã:

- Constructor CoreController: Constructor này khởi tạo một đối tượng CoreController với các tham số như con trỏ đến core cha, router, scheduler, neuron block, vector csram và vector neuron instructions.
- Phương thức getSpikes(): Phương thức này trả về một chuỗi biểu diễn các điểm nhấn (spikes) hiện tại dưới dạng chuỗi hex.
- Phương thức run(): Phương thức này thực hiện quá trình xử lý của CoreController. Đầu tiên, nó lấy các điểm nhấn hiện tại từ lập lịch (Scheduler). Sau đó, nó tính toán tích hợp và tiềm năng của mỗi neuron, kiểm tra xem neuron có phát điểm nhấn hay không, và gửi các gói tin tới router nếu có phát điểm nhấn.
- Phương thức activeConnectionIndices(): Phương thức này trả về các chỉ số của các kết nối hoạt động, nơi có cả điểm nhấn và kết nối.
- Các biến thành viên: Các biến thành viên của CoreController bao gồm con trỏ tới core cha, router, scheduler, neuron block, vector csram và vector neuron instructions.
- Quản lý ghi log: Đoạn mã cũng chứa các lệnh ghi log sử dụng thư viện plog để ghi lại quá trình thực thi của CoreController và các thông tin liên quan.

## 6 corecontroller.h
Tệp "corecontroller.h" định nghĩa lớp CoreController, một thành phần quan trọng của mỗi nhân tố cơ bản trong hệ thống xử lý cấu trúc mạng. Dưới đây là tóm tắt hoạt động của mã:

- Constructor CoreController: Constructor này khởi tạo một đối tượng CoreController với các tham số như con trỏ đến core cha, router, scheduler, neuron block, vector csram và vector neuron instructions.
- Phương thức setAxonType(): Phương thức này được sử dụng để đặt loại của một axon cụ thể trong neuron controller.
- Phương thức run(): Phương thức này thực hiện quá trình xử lý của CoreController, bao gồm tính toán tích hợp và tiềm năng của mỗi neuron, kiểm tra xem neuron có phát điểm nhấn hay không, và gửi các gói tin tới router nếu có phát điểm nhấn.
- Phương thức getSpikes(): Phương thức này trả về một chuỗi biểu diễn các điểm nhấn (spikes) hiện tại dưới dạng chuỗi.
- Các biến thành viên: Các biến thành viên của CoreController bao gồm vector neuron_instructions, vector csram, con trỏ đến scheduler, router và neuron block, và con trỏ đến core cha.
- Phương thức activeConnectionIndices(): Phương thức này trả về các chỉ số của các kết nối hoạt động, nơi có cả điểm nhấn và kết nối.
- Biến spikes: Biến này là một vector của các giá trị boolean, biểu diễn trạng thái hoạt động của các axon trong neuron controller.H

## 7 csramrow.cpp
Tệp "csramrow.cpp" định nghĩa hai constructor cho lớp CSRAMRow và một phương thức to_string(). Dưới đây là tóm tắt hoạt động của mã:

- Constructor mặc định (CSRAMRow()): Constructor này khởi tạo một đối tượng CSRAMRow với các giá trị mặc định được đọc từ các tham số trong file cấu hình.
- Constructor có tham số (CSRAMRow(std::vector<bool> connections, int current_potential, int reset_potential, int leak, int positive_threshold, int negative_threshold, std::vector<int> weights, int dx, int dy, int destination_tick, int destination_axon, int reset_mode)): Constructor này khởi tạo một đối tượng CSRAMRow với các giá trị được truyền vào từ các tham số.
- Phương thức to_string(bool hex): Phương thức này trả về một chuỗi biểu diễn các thuộc tính của CSRAMRow, bao gồm kết nối, tiềm năng hiện tại, tiềm năng reset, sự rò rỉ, ngưỡng dương, ngưỡng âm, trọng số, dx, dy, axon đích, tick đích và chế độ reset. Nếu tham số hex là true, nó sẽ trả về chuỗi dưới dạng hex, nhưng phương thức này hiện chỉ hỗ trợ trường hợp không hex.

## 8 csramrow.h
Tệp "csramrow.h" định nghĩa lớp CSRAMRow, đại diện cho một hàng CSRAM tương ứng với một neuron. Dưới đây là tóm tắt hoạt động của mã:

### a Lớp CSRAMRow:
- Lớp này lưu trữ tất cả các thông số cho một neuron trong mạng nơ-ron.
- Các thuộc tính bao gồm:

  - connections: Một vector bool lưu trữ trạng thái kết nối của các axon đến neuron này.
  - current_potential: Tiềm năng hiện tại của neuron.
  - reset_potential: Giá trị tiềm năng để reset neuron.
  - leak: Giá trị rò rỉ tiềm năng của neuron.
  - positive_threshold: Ngưỡng dương để kích hoạt neuron.
  - negative_threshold: Ngưỡng âm để kích hoạt neuron.
  - weights: Một vector chứa trọng số của các kết nối axon đến neuron này.
  - dx, dy: Độ lệch tọa độ của axon đến neuron đích.
  - destination_tick: Thời điểm (tick) mà gói tin đi đến.
  - destination_axon: Axon đích mà gói tin sẽ được gửi đến.
  - reset_mode: Chế độ reset cho neuron.
### b Constructor mặc định (CSRAMRow()): 
- Constructor này khởi tạo một đối tượng CSRAMRow với các giá trị mặc định.
### c Constructor có tham số (CSRAMRow(std::vector<bool> connections, int current_potential, int reset_potential, int leak, int positive_threshold, int negative_threshold, std::vector<int> weights, int dx, int dy, int -- destination_tick, int destination_axon, int reset_mode)): 
- Constructor này khởi tạo một đối tượng CSRAMRow với các giá trị được truyền vào từ các tham số.
### d Phương thức to_string(bool hex): 
- Phương thức này trả về một chuỗi biểu diễn các thuộc tính của CSRAMRow. Nếu tham số hex là true, nó sẽ trả về chuỗi dưới dạng hex.

### 9 decode.hpp
Code này là một tập hợp các hàm được sử dụng để giải mã dữ liệu đầu vào từ tệp JSON vào các đối tượng và cấu trúc dữ liệu khác nhau trong chương trình. Dưới đây là tóm tắt về mỗi chức năng chính:

- InputDecodingException: Lớp ngoại lệ được sử dụng để xử lý các ngoại lệ phát sinh trong quá trình giải mã dữ liệu đầu vào.
- parsePacketDestinationCore: Phân tích các giá trị liên quan đến điểm đến của gói tin trong một vòng lặp.
- parsePacketDestinationAxon: Phân tích giá trị liên quan đến axon đích của gói tin.
- parsePacketDestinationTick: Phân tích giá trị liên quan đến điểm đến tick của gói tin.
- parseInputPackets: Phân tích các gói tin đầu vào từ tệp JSON, trả về một vector chứa các vector gói tin cho mỗi tick.
- parseCoreCoordinates: Phân tích tọa độ của lõi từ dữ liệu JSON.
- parseCoreNeurons: Phân tích các thông số liên quan đến neurons của lõi từ dữ liệu JSON.
- parseCoreConnections: Xác nhận rằng các kết nối trong lõi được thiết lập đúng.
- parseCoreNeuronInstructions: Phân tích các hướng dẫn của neurons trong lõi từ dữ liệu JSON.
- parseNeuronConnections: Phân tích các kết nối của neurons từ dữ liệu JSON.
- parseNeuronWeights: Phân tích trọng số của neurons từ dữ liệu JSON.
- parseNeuronDestinationCore: Phân tích điểm đến core của neurons từ dữ liệu JSON.
- parseNeuronDestinationAxon: Phân tích axon đích của neurons từ dữ liệu JSON.
- parseNeuronDestinationAxonOutputBus: Phân tích axon đích của neurons khi nó kết nối với output bus.
- parseNeuronDestinationTick: Phân tích điểm đến tick của neurons từ dữ liệu JSON.
- parseNeuronParameter: Phân tích các tham số khác của neurons từ dữ liệu JSON.
- parseOutputBus: Phân tích dữ liệu đầu vào của output bus từ tệp JSON.
- parseCores: Phân tích dữ liệu đầu vào của các lõi từ tệp JSON và xây dựng các đối tượng lõi và kết nối chúng với nhau.

## 10 main.cpp
Code này là chương trình chính của mô phỏng RANC (Reconfigurable Asynchronous Neuromorphic Computing). Dưới đây là tóm tắt về cách chương trình hoạt động:

- Xác định các tham số dòng lệnh: Chương trình sử dụng thư viện cxxopts để xác định các tham số dòng lệnh như tên tệp đầu vào, tên tệp đầu ra, tệp cấu hình, số lượng ticks cần chạy, tên tệp trace và tần suất báo cáo.
- Xác định tệp cấu hình: Dữ liệu cấu hình được đọc từ tệp JSON được chỉ định và lưu trữ trong một biến toàn cục.
- Xác định tệp đầu vào và đầu ra: Tên tệp đầu vào và đầu ra được xác định từ các tham số dòng lệnh. Nếu không có tệp nào được chỉ định, chương trình sẽ kết thúc và in ra hướng dẫn sử dụng.
- Khởi tạo các thành phần: Dữ liệu đầu vào từ tệp JSON được giải mã bằng cách sử dụng các hàm trong module decode.hpp để tạo ra các đối tượng và cấu trúc dữ liệu cần thiết cho mô phỏng.
- Bắt đầu mô phỏng: Các đối tượng được tạo ra từ dữ liệu đầu vào được sử dụng để khởi tạo một lưới RANC. Sau đó, mô phỏng được bắt đầu với số lượng ticks được chỉ định và tần suất báo cáo.
