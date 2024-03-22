import jpcap.JpcapCaptor;
import jpcap.NetworkInterface;
import jpcap.PacketReceiver;
import jpcap.packet.*;

public class NetworkTrafficAnalyzer {

    public static void main(String[] args) {
        try {
            // Get list of network interfaces
            NetworkInterface[] devices = JpcapCaptor.getDeviceList();
            if (devices.length == 0) {
                System.out.println("No network interface found");
                return;
            }

            // Choose a network interface to capture packets
            NetworkInterface device = devices[0]; // Choose the first interface

            // Open the capture device
            JpcapCaptor captor = JpcapCaptor.openDevice(device, 65535, true, 20);

            // Create a packet receiver
            PacketReceiver receiver = new PacketReceiver() {
                @Override
                public void receivePacket(Packet packet) {
                    if (packet instanceof IPPacket) {
                        IPPacket ipPacket = (IPPacket) packet;
                        String srcIp = ipPacket.src_ip.toString();
                        String dstIp = ipPacket.dst_ip.toString();
                        int protocol = ipPacket.protocol;

                        System.out.println("Source IP: " + srcIp + ", Destination IP: " + dstIp + ", Protocol: " + protocol);
                    }
                }
            };

            // Start capturing packets
            captor.loopPacket(-1, receiver);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
