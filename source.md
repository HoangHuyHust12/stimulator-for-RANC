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
Trả về một chuỗi mô tả vị trí của core trong mạng.
- Phương thức prepare():
Gọi phương thức updateCurrentWord() của Scheduler để cập nhật từ hiện tại.
- Phương thức run():
Gọi phương thức run() của CoreController để thực thi logic xử lý của core.
- Phương thức receivePacket(Packet packet):
Gọi phương thức receivePacket(Packet packet) của Scheduler để xử lý gói tin được nhận.

Tóm lại, đoạn mã này thực hiện việc khởi tạo và quản lý các thành phần chính của một core trong hệ thống xử lý cấu trúc mạng, bao gồm định nghĩa các phương thức để chuẩn bị, thực thi và xử lý các gói tin.

## 4 core.h
Đoạn mã trong file "core.h" định nghĩa lớp Core, đại diện cho một nhân tố cơ bản trong hệ thống xử lý cấu trúc mạng. Dưới đây là tóm tắt hoạt động của mã:

- Định nghĩa lớp Core: Lớp Core được kế thừa từ lớp Component, đảm bảo rằng các đối tượng Core có các phương thức cơ bản như prepare(), run(), và receivePacket(Packet packet).
- Các constructors: Có nhiều phiên bản constructor cho phép tạo đối tượng Core với các cấu hình khác nhau. Các tham số của các constructors này cho phép xác định các core lân cận, bộ nhớ CSRAM, hướng dẫn neuron, vị trí của core, loại và giá trị reset của neuron.
- Phương thức prepare(): Được kế thừa từ lớp Component, phương thức này được gọi để chuẩn bị core trước khi chạy.
- Phương thức run(): Được kế thừa từ lớp Component, phương thức này chạy logic xử lý của core.
- Phương thức receivePacket(Packet packet): Được kế thừa từ lớp Component, phương thức này được gọi khi core nhận được một gói tin.
- Phương thức to_string(): Trả về một chuỗi mô tả vị trí của core trong mạng.
- Các thành phần của Core: Scheduler, NeuronBlock, và CoreController là các thành phần chính của một core trong hệ thống xử lý cấu trúc mạng.

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
- Bắt đầu mô phỏng: Các đối tượng được tạo ra từ dữ liệu đầu vào được sử dụng để khởi tạo một mạng RANC. Sau đó, mô phỏng được bắt đầu với số lượng ticks được chỉ định và tần suất báo cáo.

## 11 neuronblock.cpp
Code này định nghĩa lớp NeuronBlock đại diện cho một khối neuron trong một mạng neural. Dưới đây là tóm tắt về cách lớp này hoạt động:

- Constructor: Lớp có 3 constructor khác nhau, cho phép khởi tạo NeuronBlock với các giá trị mặc định hoặc được chỉ định.
- Phương thức integrate: Phương thức này tích hợp các trọng số synapse vào điện thế hiện tại của neuron bằng cách cộng dồn các giá trị synapse tương ứng.
- Phương thức leak: Phương thức này mô phỏng sự rò rỉ điện từ của neuron bằng cách cộng thêm một giá trị rò rỉ vào điện thế hiện tại.
- Phương thức spikes: Phương thức này kiểm tra xem điện thế hiện tại của neuron có vượt ngưỡng dương không để xác định xem neuron có phát xung hay không.
- Phương thức output_potential: Phương thức này tính toán và trả về điện thế đầu ra của neuron sau một vòng lặp tích hợp và rò rỉ. Điện thế đầu ra có thể được điều chỉnh dựa trên các ngưỡng dương và âm, điểm reset, và chế độ reset được chỉ định. Điện thế đầu ra được tính toán theo các luật reset được chỉ định (asymetric hoặc symetric reset).

## 12 neuronblock.h
File header neuronblock.h định nghĩa lớp NeuronBlock và các thành phần liên quan. Dưới đây là tóm tắt về cấu trúc và chức năng của file này:

- Nguyên tắc đặt tên đối tượng:
  - NeuronBlock: Đại diện cho một khối neuron trong một mạng neural.
  - reset_types: Liệt kê các loại reset khác nhau cho neuron, bao gồm asymetric_reset và symetric_reset.
  - reset_modes: Liệt kê các chế độ reset khác nhau cho neuron, bao gồm absolute_reset và linear_reset.
- Các thành phần của lớp NeuronBlock:
  - Constructors: Có ba hàm tạo khác nhau để khởi tạo đối tượng NeuronBlock với các giá trị mặc định hoặc được chỉ định.
  - Phương thức integrate: Thực hiện phép tích hợp giá trị synapse vào điện thế hiện tại của neuron.
  - Phương thức leak: Thực hiện phép rò rỉ điện từ của neuron.
  - Phương thức spikes: Kiểm tra xem neuron có phát xung hay không dựa trên điện thế hiện tại.
  - Phương thức output_potential: Tính toán và trả về điện thế đầu ra của neuron dựa trên các ngưỡng và chế độ đặt lại được chỉ định.
- Biến thành viên:
  - current_potential: Điện thế hiện tại của neuron.
  - reset_type: Loại đặt lại được sử dụng cho neuron.
Đây là một cấu trúc cơ bản để mô phỏng hoạt động của một khối neuron trong một mạng neural.

## 13 outputbus.cpp
File outputbus.cpp định nghĩa các phương thức của lớp OutputBus, một thành phần của kiến trúc mạng RANC. Dưới đây là tóm tắt về hoạt động của mã:

- Constructor:
  - Có hai hàm tạo khác nhau cho đối tượng OutputBus.
  - Hàm tạo đầu tiên không tham số tạo ra một OutputBus với một router không được kết nối với bất kỳ thành phần nào khác.
  - Hàm tạo thứ hai khởi tạo một OutputBus với các đối tượng thành phần kết nối (phía bắc, phía nam, phía tây, phía đông), số lượng đầu ra, vị trí x và y.
- Phương thức receivePacket:
  - Nhận một gói tin từ router và xác định xem có spike không dựa trên đích đến của gói tin.
  - Nếu đã có spike cho đích đến, thông báo về việc nhận nhiều spike cho cùng một axon.
- Phương thức prepare:
  - Chuẩn bị dữ liệu trước khi chuyển đi.
  - Ghi lại trạng thái của các spikes hiện tại vào đầu ra.
- Phương thức run:
  - Không thực hiện hoạt động gì.
  - Được gọi từ hệ thống quản lý hoạt động của kiến trúc RANC, nhưng không có hoạt động cụ thể được thực hiện trong phương thức này.
- Biến thành viên:
  - router: Một địa chỉ của router mà bus này kết nối đến.
  - x, y: Vị trí của bus trên mạng.
  - num_outputs: Số lượng đầu ra của bus.
  - spikes: Một vector bool lưu trữ trạng thái của spikes cho mỗi đầu ra.
 
## 14 outputbus.h
File outputbus.h định nghĩa lớp OutputBus và các thành phần của nó. Dưới đây là tóm tắt về hoạt động của mã:

- Class OutputBus:
  - Là một lớp con của lớp Component, cho phép OutputBus tham gia vào hệ thống kiến trúc RANC.
  - Định nghĩa hai hàm tạo: một không có tham số và một có các tham số để khởi tạo các đối tượng OutputBus.
  - Định nghĩa các phương thức:
    - prepare(): Chuẩn bị dữ liệu cho việc truyền đi.
    - run(): Thực hiện hoạt động của bus (trong trường hợp này, không có hoạt động cụ thể).
    - receivePacket(Packet packet): Nhận một gói tin từ router.
    - logOutputs(): Ghi lại trạng thái của đầu ra (không được định nghĩa trong file này).
  - Có các biến thành viên:
    - num_outputs: Số lượng đầu ra của bus.
    - spikes: Một vector bool lưu trữ trạng thái của spikes cho mỗi đầu ra.
   
## 15 packet.cpp 
File packet.cpp định nghĩa các phương thức của lớp Packet. Dưới đây là tóm tắt về hoạt động của mã:

-Constructor:
  - Constructor nhận các tham số để khởi tạo một đối tượng Packet, bao gồm dx (delta x), dy (delta y), delivery_tick (thời điểm giao hàng), và destination_axon (axon đích).
- Các phương thức:
  - incrementDx(): Tăng giá trị của dx lên một đơn vị.
  - decrementDx(): Giảm giá trị của dx đi một đơn vị.
  - incrementDy(): Tăng giá trị của dy lên một đơn vị.
  - decrementDy(): Giảm giá trị của dy đi một đơn vị.
  - to_string(): Trả về một chuỗi biểu diễn thông tin về đối tượng Packet dưới dạng "dx: {dx}, dy: {dy}, delivery_tick: {delivery_tick}, destination_axon: {destination_axon}".

## 16 packet.h
File packet.h chứa khai báo lớp Packet cùng các thành phần dữ liệu và phương thức của nó. Dưới đây là tóm tắt về hoạt động của mã:

Class Packet:
- Lớp này đại diện cho một gói tin trong hệ thống.
- Các thành phần dữ liệu bao gồm:
  - dx: Delta x - sự thay đổi về tọa độ x.
  - dy: Delta y - sự thay đổi về tọa độ y.
  - delivery_tick: Thời điểm giao hàng - thời điểm mà gói tin được gửi đi.
  - destination_axon: Axon đích - đích đến của gói tin.
- Các phương thức bao gồm:
  - Packet(int dx, int dy, int delivery_tick, int destination_axon): Constructor để khởi tạo một đối tượng Packet với các giá trị ban đầu.
  - incrementDx(): Tăng giá trị của dx.
  - decrementDx(): Giảm giá trị của dx.
  - incrementDy(): Tăng giá trị của dy.
  - decrementDy(): Giảm giá trị của dy.
  - to_string(): Trả về một chuỗi biểu diễn thông tin về gói tin dưới dạng "dx: {dx}, dy: {dy}, delivery_tick: {delivery_tick}, destination_axon: {destination_axon}".
File này chỉ chứa khai báo của lớp Packet mà không có định nghĩa chi tiết của các phương thức, các phương thức này được định nghĩa trong file packet.cpp.

## 17 rancgrid.cpp
File RANCGrid.cpp định nghĩa các phương thức của lớp RANCGrid, bao gồm constructor và phương thức beginActivity để bắt đầu hoạt động của mạng RANC.

- Constructor RANCGrid::RANCGrid:
  - Constructor này khởi tạo một đối tượng RANCGrid với các gói tin đầu vào và các thành phần của mạng RANC.
- Phương thức RANCGrid::beginActivity:
  - Phương thức này bắt đầu hoạt động của mạng RANC trong một số ticks cụ thể.
  - Trong phương thức này:
    - In ra thông báo về việc bắt đầu mô phỏng với số ticks đã cho.
    - Gửi các gói tin đầu vào ban đầu tới thành phần đầu tiên của mạng.
    - Lặp qua từng tick và thực hiện các bước sau:
    - Chuẩn bị các thành phần cho tick tiếp theo.
    - Nhận các gói tin spike đầu vào và gửi tới thành phần đầu tiên của mạng.
    - Lặp qua từng thành phần của mạng và thực hiện phương thức run() của chúng để mô phỏng hoạt động của các nhóm neuron.
   
## 18 rancgrid.h
File RANCGrid.h định nghĩa lớp RANCGrid, đại diện cho mạng RANC trong một mô phỏng hoạt động. Dưới đây là tóm tắt hoạt động của code:

- Class RANCGrid:
  - Lớp này đại diện cho mạng RANC và chứa các thành phần và gói tin đầu vào cần thiết cho mô phỏng hoạt động của mạng.
- Constructor RANCGrid(std::vector<std::vector<Packet>> input_packets, std::vector<Component*> components):
  - Constructor này khởi tạo một đối tượng RANCGrid với các gói tin đầu vào và danh sách các thành phần của mạng.
- Phương thức beginActivity(int num_ticks, int report_frequency):
  - Phương thức này bắt đầu hoạt động của mạng RANC trong một số ticks cụ thể.
  - Trong phương thức này:
    - Các gói tin đầu vào được gửi tới mạng RANC trước khi bắt đầu mô phỏng.
    - mạng RANC được mô phỏng qua một chuỗi các ticks, trong mỗi tick, các thành phần của mạng được chuẩn bị và sau đó hoạt động được thực hiện.

## 19 router.cpp
File router.cpp triển khai các phương thức của lớp Router, một phần của hệ thống định tuyến của mạng mạng RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor Router(Component* parent, Router* north, Router* south, Router* west, Router* east):
  - Constructor này khởi tạo một định tuyến Router với các định tuyến hàng xóm được chỉ định.
- Phương thức receiveLocal(Packet packet):
  - Phương thức này xử lý gói tin nhận được từ bên trong mạng RANC.
- Các phương thức receiveWest(Packet packet), receiveEast(Packet packet), receiveSouth(Packet packet), receiveNorth(Packet packet):
  - Nhận gói tin từ các hướng hàng xóm tương ứng và chuyển tiếp chúng.
- Các phương thức receiveLocalOrEast(Packet packet), receiveLocalOrWest(Packet packet), forwardLocal(Packet packet), forwardEast(Packet packet), forwardWest(Packet packet), forwardNorth(Packet packet),
forwardSouth(Packet packet), forwardSouthOrLocal(Packet packet), forwardNorthOrLocal(Packet packet):
  - Xử lý việc chuyển tiếp gói tin đến hoặc từ các hướng hàng xóm và bên trong mạng RANC.
- Phương thức to_string():
  - Trả về thông tin về tọa độ của định tuyến, được sử dụng cho mục đích ghi log và debug.

 ## 20 router.h 
 File router.h định nghĩa lớp Router, một thành phần quan trọng trong hệ thống định tuyến của mạng mạng RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor Router(Component* parent, Router* north, Router* south, Router* west, Router* east):
  - Constructor này khởi tạo một định tuyến Router với một con trỏ tới thành phần cha và các con trỏ tới các định tuyến hàng xóm.
- Các phương thức nhận gói tin (receiveLocal, receiveWest, receiveEast, receiveSouth, receiveNorth):
  - Các phương thức này nhận các gói tin từ các hướng khác nhau và chuyển tiếp chúng tới các hướng khác hoặc đối tượng parent (Component).
- Các phương thức chuyển tiếp gói tin (forwardEast, forwardWest, forwardNorth, forwardSouth, forwardLocal):
  - Các phương thức này chuyển tiếp các gói tin tới các định tuyến hàng xóm hoặc đối tượng parent (Component).
- Các phương thức receiveLocalOrEast, receiveLocalOrWest, forwardSouthOrLocal, forwardNorthOrLocal:
  - Các phương thức này xử lý việc nhận và chuyển tiếp gói tin tùy thuộc vào hướng đi của chúng.
- Phương thức to_string():
  - Trả về một chuỗi mô tả tọa độ của định tuyến, được sử dụng cho mục đích ghi log và debug.
- Các biến thành viên:
  - parent: Con trỏ đến thành phần cha của định tuyến.
  - north, south, east, west: Con trỏ tới các định tuyến hàng xóm.

## 21 scheduler.cpp
File scheduler.cpp triển khai các phương thức của lớp Scheduler, một thành phần quản lý việc lập lịch trong hệ thống mạng mạng RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor Scheduler(Core* parent):
  - Constructor này khởi tạo một Scheduler với một con trỏ tới Core cha và tạo một đối tượng SchedulerSRAM tương ứng.
- Phương thức receivePacket(Packet packet):
  - Nhận một gói tin và ghi nó vào SchedulerSRAM theo thời gian giao hàng và axon đích.
- Phương thức getSpikes():
  - Trả về các tín hiệu từ SchedulerSRAM cho từng từ hiện tại.
- Phương thức clear():
  - Xóa dữ liệu trong từ hiện tại của SchedulerSRAM.
- Phương thức updateCurrentWord():
  - Cập nhật từ hiện tại trong SchedulerSRAM.

## 22 scheduler.h 
File scheduler.h định nghĩa lớp Scheduler, đại diện cho thành phần quản lý lập lịch trong hệ thống mạng mạng RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor Scheduler(Core* parent):
  - Constructor này khởi tạo một Scheduler với một con trỏ tới Core cha.
- Phương thức receivePacket(Packet packet):
  - Nhận một gói tin và chuyển tiếp nó cho SchedulerSRAM để lưu trữ.
- Phương thức clear():
  - Xóa dữ liệu hiện tại trong SchedulerSRAM.
- Phương thức updateCurrentWord():
  - Cập nhật từ hiện tại trong SchedulerSRAM.
- Phương thức getSpikes():
  - Trả về các tín hiệu từ SchedulerSRAM cho từng từ hiện tại.
- Biến Core* parent:
  - Con trỏ tới Core cha của Scheduler, cho phép nó truy cập các thành phần khác trong hệ thống.
 
## 23 schedulersram.cpp
File schedulersram.cpp định nghĩa các phương thức của lớp SchedulerSRAM, một thành phần quản lý bộ nhớ RAM tĩnh (SRAM) được sử dụng bởi Scheduler trong hệ thống mạng mạng RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor SchedulerSRAM(Scheduler* scheduler):
  - Constructor này khởi tạo một SchedulerSRAM với một con trỏ tới Scheduler cha.
  - Khởi tạo một ma trận boolean để lưu trữ dữ liệu, với kích thước dựa trên các thông số được cấu hình trong Config.
- Phương thức getCurrentWord():
Trả về từ hiện tại từ SRAM.
- Phương thức write(int word, int bit):
  - Ghi một bit vào từ được chỉ định của SRAM.
  - Kiểm tra để tránh ghi vào từ hiện tại.
  - Xử lý trường hợp ghi trùng lặp hoặc ghi vào từ không hợp lệ.
  - Ghi bit vào SRAM.
- Phương thức clearCurrentWord():
  - Xóa tất cả các bit trong từ hiện tại của SRAM.
- Phương thức updateCurrentWord():
  - Cập nhật chỉ số của từ hiện tại của SRAM, chuyển sang từ tiếp theo.
  - Ghi log các thông tin cần thiết nếu được cấu hình.
- Phương thức to_string():
  - Trả về một chuỗi biểu diễn của dữ liệu SRAM dưới dạng chuỗi hex.
 
## 24 schedulersram.h
File schedulersram.h định nghĩa lớp SchedulerSRAM, đại diện cho bộ nhớ RAM tĩnh được sử dụng bởi Scheduler trong hệ thống mạng lưới RANC. Dưới đây là tóm tắt hoạt động của code:

- Constructor SchedulerSRAM(Scheduler* scheduler):
  - Constructor này khởi tạo một đối tượng SchedulerSRAM với con trỏ đến Scheduler cha.
- Phương thức write(int word, int bit):
  - Ghi một bit vào vị trí được chỉ định trong từ của SRAM.
- Phương thức getCurrentWord():
  - Trả về từ hiện tại từ SRAM.
- Phương thức clearCurrentWord():
  - Xóa tất cả các bit trong từ hiện tại của SRAM.
- Phương thức updateCurrentWord():
  - Cập nhật chỉ số của từ hiện tại của SRAM để trỏ đến từ tiếp theo.
- Phương thức to_string():
  - Trả về một chuỗi biểu diễn của dữ liệu SRAM dưới dạng chuỗi.
