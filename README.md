# Stimulator for RANC
stimulator for RANC

## 1) Example 
- Packets chứa list packets , mỗi packet có điểm đích là core, axon, và tick.
- Output_bus chỉ định các tọa độ (coordinates) và số lượng output.
- Cores chứa thông tin về cores, bao gồm axons, neurons, và connections.

## 2) mceliece 
Đoạn mã này mô tả một hệ thống nơ-ron nhân tạo được tổ chức thành các nhân tố như nhân tố reset_potential, weights, leak, positive_threshold, negative_threshold, destination_core_offset, destination_axon, destination_tick, current_potential, và reset_mode. Có hai nhóm nhân tố chính là "cores" và "output_bus":

- "Cores" là các nhóm nơ-ron được đặt ở các tọa độ trong không gian. Mỗi nhóm nơ-ron bao gồm các thông số của nơ-ron như weights, leak, positive_threshold, negative_threshold, và các kết nối với các nhóm nơ-ron khác thông qua connections.

- "Output_bus" là một đầu ra có tọa độ cụ thể và số lượng đầu ra.

"Packets" chứa các gói tin được gửi từ một nhóm nơ-ron đến một nhóm nơ-ron khác, được xác định bằng tọa độ của nhóm nơ-ron đích, axon đích, và tick của gói tin.

## 3) VMM
### 3.1) josh-inputjson
Đoạn mã này mô tả một hệ thống nơ-ron nhân tạo được đặt ở các tọa độ khác nhau trong không gian.

- Mỗi nhóm nơ-ron bao gồm các nơ-ron ("neurons") với các thông số như reset_potential, weights, leak, positive_threshold, negative_threshold, destination_core_offset, destination_axon, destination_tick, current_potential, và reset_mode.

- Các nơ-ron kết nối với nhau thông qua mạng lưới connections.

- Một output_bus được định nghĩa với số lượng đầu ra cụ thể và các tọa độ.

- Cuối cùng, có một số gói tin được gửi từ một nhóm nơ-ron đến một nhóm nơ-ron khác, được xác định bằng tọa độ của nhóm nơ-ron đích, axon đích, và tick của gói tin.

### 3.2 test.json
Đoạn mã này mô tả một hệ thống nơ-ron nhân tạo với một nhóm nơ-ron ("cores") đặt ở tọa độ [0, 0] trong không gian.

- Nhóm nơ-ron này bao gồm các nơ-ron ("neurons") với các thông số như reset_potential, weights, leak, positive_threshold, negative_threshold, destination_core, destination_axon, destination_tick, current_potential, và reset_mode.

- Các nơ-ron kết nối với nhau thông qua mạng lưới connections.

- Ngoài ra, có một output_bus được định nghĩa với số lượng đầu ra cụ thể và các tọa độ là [1, 0].

- Cuối cùng, có một số gói tin được gửi từ nhóm nơ-ron này đến chính nó, được xác định bằng tọa độ của nhóm nơ-ron đích, axon đích, và tick của gói tin.
