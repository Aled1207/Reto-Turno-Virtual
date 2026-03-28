# Reto-Turno-Virtual

1ra Clase: TurnoVirtual.
_____________________________________

package com.mycompany.turnovirtual;

/**
 * 
 * @author ALED .D
 */
public class TurnoVirtual {

    public static void main(String[] args) {
        
    }
    private String[] turnos;
    private String[] turnosPerdidos;
    private boolean estadoTurnoVirtual;
    private int turnoEnAtencion;
    private int cantidadTurnosAtendidos;

    public TurnoVirtual(String[] turnos) {
        this.turnos = turnos;
        this.turnosPerdidos = new String[turnos.length];
        for (int i = 0; i < turnosPerdidos.length; i++) {
            turnosPerdidos[i] = " ";
        }
        this.estadoTurnoVirtual = true;
        this.turnoEnAtencion = 0;
        this.cantidadTurnosAtendidos = 1;
    }

    public void atenderProximoTurno() {
        if (estadoTurnoVirtual == true) {
            turnoEnAtencion++;
            cantidadTurnosAtendidos++;
        }
    }

    public void agregarTurnoPerdido() {
        turnosPerdidos[turnoEnAtencion] = turnos[turnoEnAtencion];
    }

    public void cambiarEstadoTurno() {
        estadoTurnoVirtual = estadoTurnoVirtual != true;
    }

    public String[] getTurnos() {
        return turnos;
    }

    public void setTurnos(String[] turnos) {
        this.turnos = turnos;
    }

    public String[] getTurnosPerdidos() {
        return turnosPerdidos;
    }

    public void setTurnosPerdidos(String[] turnosPerdidos) {
        this.turnosPerdidos = turnosPerdidos;
    }

    public boolean isEstadoTurnoVirtual() {
        return estadoTurnoVirtual;
    }

    public void setEstadoTurnoVirtual(boolean estadoTurnoVirtual) {
        this.estadoTurnoVirtual = estadoTurnoVirtual;
    }

    public int getTurnoEnAtencion() {
        return turnoEnAtencion;
    }

    public void setTurnoEnAtencion(int turnoEnAtencion) {
        this.turnoEnAtencion = turnoEnAtencion;
    }

    public int getCantidadTurnosAtendidos() {
        return cantidadTurnosAtendidos;
    }

    public void setCantidadTurnosAtendidos(int cantidadTurnosAtendidos) {
        this.cantidadTurnosAtendidos = cantidadTurnosAtendidos;
    }
}
_____________________________________________________________________

2da clase: MAIN
_____________________________________________________________________

package com.mycompany.turnovirtual;

import java.util.Arrays;
import java.util.Scanner;
/**
 *  
 * @author ALED .D
 */
public class Main {
      public static void main(String[] args) {

          // ===== PEDIR CANTIDAD DE TURNOS =====
          try (Scanner sc = new Scanner(System.in)) {
              // ===== PEDIR CANTIDAD DE TURNOS =====
              System.out.print("¿Cuantos turnos desea agregar?: ");
              int cantidad = sc.nextInt();
              sc.nextLine(); // limpiar buffer
              
              // ===== PEDIR LOS TURNOS =====
              String[] cola = new String[cantidad];
              
              for (int i = 0; i < cantidad; i++) {
                  System.out.print("Ingrese el turno " + (i + 1) + ": ");
                  cola[i] = sc.nextLine();
              }
              
              // ===== CREAR OBJETO =====
              TurnoVirtual tv = new TurnoVirtual(cola);
              
              // ===== MENU DE OPCIONES =====
              int opcion = 0;
              
              while (opcion != 5) {
                  System.out.println("\n===== MENU =====");
                  System.out.println("1. Atender siguiente turno");
                  System.out.println("2. Agregar turno perdido");
                  System.out.println("3. Cambiar estado del turno");
                  System.out.println("4. Ver estado actual");
                  System.out.println("5. Salir");
                  System.out.print("Elige una opcion: ");
                  opcion = sc.nextInt();
                  
                  switch (opcion) {
                      case 1:
                          tv.atenderProximoTurno();
                          System.out.println(" Turno atendido!");
                          break;
                          
                      case 2:
                          tv.agregarTurnoPerdido();
                          System.out.println(" Turno marcado como perdido!");
                          break;
                          
                      case 3:
                          tv.cambiarEstadoTurno();
                          if (tv.isEstadoTurnoVirtual()) {
                              System.out.println(" Turno Virtual ABIERTO");
                          } else {
                              System.out.println(" Turno Virtual CERRADO");
                          }
                          break;
                          
                      case 4:
                          System.out.println("\n===== ESTADO ACTUAL =====");
                          System.out.print("Turnos: ");
                          System.out.println(Arrays.toString(tv.getTurnos()));
                          System.out.print("Turnos Perdidos: ");
                          System.out.println(Arrays.toString(tv.getTurnosPerdidos()));
                          System.out.print("Estado del Turno Virtual: ");
                          System.out.println(tv.isEstadoTurnoVirtual());
                          System.out.print("Turno en Atencion: ");
                          System.out.println(tv.getTurnoEnAtencion());
                          System.out.print("Cantidad de turnos atendidos: ");
                          System.out.println(tv.getCantidadTurnosAtendidos());
                          break;
                          
                      case 5:
                          System.out.println(" Saliendo...");
                          break;
                          
                      default:
                          System.out.println(" Opcion no valida");
                          break;
                  }
              } }
    }
}
