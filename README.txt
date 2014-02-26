The BT module has following services/characteristics/ which are used in this project:

Service: 0000ffe0-0000-1000-8000-00805f9b34fb
         Characteristic: 0000ffe4-0000-1000-8000-00805f9b34fb   --> read data from module.
                Property: Notify. (so we can notify the phone via onNotify call back, the sample is using onCharecteristicchange() which is an alternative.)

Service: 0000ffe5-0000-1000-8000-00805f9b34fb
         Characteristic: 0000ffe9-0000-1000-8000-00805f9b34fb   --> read data from module.
                Property: Write. (so we can write "x" to the module as a "ready to receive" signal.)

The UUID to name mapping is done in SampleAttributes.java, which is a nice design.

There are a few important things you may want to know about ble.

Basic procedures using BLE.
1. get the ble device.
2. get all the services and characteristics.
3. loop through those services and characteristics to find desired characteristic in our case "read" and "write".
4. for read set the notification: mBluetoothLeService.setCharacteristicNotification(characteristic, true);
5. to write characteristic, you need to mCharacteristic.setValue() first, and then trigger writeCharacteristic(mCharacteristic).
Refer to BluetoothLeService.java --> public void writeCharacteristic(BluetoothGattCharacteristic characteristic, String stringData) for more detail.
6. the major task is to implement the callback function. Refer to(BluetoothLeService.java): private final BluetoothGattCallback mGattCallback = new BluetoothGattCallback() {
