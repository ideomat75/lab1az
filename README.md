# lab1az
public class FirstTask
{
    public static void Solution()
    {
        Console.WriteLine("Min sbyte: " + SByte.MinValue + " Max sbyte: " + SByte.MaxValue);
        Console.WriteLine("Min byte: " + Byte.MinValue + " Max byte: " + Byte.MaxValue);
        Console.WriteLine("Min short: " + Int16.MinValue + " Max short: " + Int16.MaxValue);
        Console.WriteLine("Min ushort: " + UInt16.MinValue + " Max ushort: " + UInt16.MaxValue);
        Console.WriteLine("Min int: " + Int32.MinValue + " Max int: " + Int32.MaxValue);
        Console.WriteLine("Min uint: " + UInt32.MinValue + " Max uint: " + UInt32.MaxValue);
        Console.WriteLine("Min long: " + Int64.MinValue + " Max long: " + Int64.MaxValue);
        Console.WriteLine("Min ulong: " + UInt64.MinValue + " Max ulong: " + UInt64.MaxValue);
        Console.WriteLine("Min nint: " + IntPtr.MinValue + " Max nint: " + IntPtr.MaxValue);
        Console.WriteLine("Min nuint: " + UIntPtr.MinValue + " Max nuint: " + UIntPtr.MaxValue);

        Console.WriteLine("Min float: " + Single.MinValue + " Max float: " + Single.MaxValue);
        Console.WriteLine("Min double: " + Double.MinValue + " Max double: " + Double.MaxValue);
        Console.WriteLine("Min decimal: " + Decimal.MinValue + " Max decimal: " + Decimal.MaxValue);

        Console.WriteLine("Min char: " + Char.MinValue + " Max char: " + Char.MaxValue);

        Console.WriteLine("boolean: " + Boolean.FalseString + " ; " + Boolean.TrueString);
    }
}



// task_2

public class Rectangle
{
    private double side1, side2;
    private double area, perimeter;
    
    public double Area
    {
        get { return AreaCalculator(); }
    }
    
    public double Perimeter
    {
        get { return PerimeterCalculator(); }
    }
    
    public Rectangle(double sideA, double sideB)
    {
        side1 = sideA; 
        side2 = sideB;
    }

    public double AreaCalculator()
    {
        return side1 * side2;
    }

    public double PerimeterCalculator()
    {
        return 2 * (side1 + side2);
    }
}

public class Point
{
    private int x, y;

    public int X
    {
        get { return x; }
    }

    public int Y
    {
        get { return y; }
    }

    public Point(int pX, int pY)
    {
        x = pX;
        y = pY;
    }
}
//task 3
public class Figure
{
    private Point p1, p2, p3, p4, p5;
    private string _name;
    public string Name { get; set; }
    public Figure(Point P1, Point P2, Point P3)
    {
        p1 = P1;
        p2 = P2;
        p3 = P3;
    }
    
    public Figure(Figure f, Point P4) : this(f.p1, f.p2, f.p3)
    {
        p4 = P4;
    }

    public Figure(Figure f, Point P4, Point P5) : this(f.p1, f.p2, f.p3)
    {
        p4 = P4;
        p5 = P5;
    }

    public double LengthSide(Point A, Point B)
    {
        double a = B.X - A.X;
        double b = B.Y - A.Y;
        a = a * a;
        b = b * b;
        return Math.Sqrt(a + b);
    }

    public void PerimeterCalculator()
    {
        double a = LengthSide(p1, p2);
        double b = LengthSide(p2, p3);
        
        if (Name == "треугольник")
        {
            double c = LengthSide(p3, p1);
            Console.WriteLine("Периметр треугольника: " + (a+b+c));
            
        }
        else if (Name == "четырехугольник")
        {
            double c = LengthSide(p3, p4);
            double d = LengthSide(p4, p1);
            Console.WriteLine("Периметр четырехугольника: " + (a+b+c+d));
        }
        else if (Name == "пятиугольник")
        {
            double c = LengthSide(p3, p4);
            double d = LengthSide(p4, p5);
            double e = LengthSide(p5, p1);
            Console.WriteLine("Периметр пятиугольника: " + (a+b+c+d+e));
        }
        else
        {
            Console.WriteLine("Такой фигуры у нас нет");
            Environment.Exit(0);
        }
    }
}

class Test
{
    static void Main(string[] args)
    {
        Console.Write("Введите номер задания: ");
        string? n = Console.ReadLine();
        if (n == "1")
        {
            // t1
            FirstTask.Solution();
        }
        else if (n == "2")
        {
            //t2
            double s1;
            double s2;
            Console.Write("Введите длину первой стороны: ");
            string? s1_tmp = Console.ReadLine();
            Console.Write("Введите длину второй стороны: ");
            string? s2_tmp = Console.ReadLine();
            bool check = double.TryParse(s1_tmp, out s1) & double.TryParse(s2_tmp, out s2);
            if (check == false || s1 <= 0 || s2 <= 0)
            {
                Console.WriteLine("Данные введены неверно");
                Environment.Exit(0);
            }

            var rectangle = new Rectangle(s1, s2);
            Console.WriteLine("Площадь прямоугольника: " + rectangle.Area + "\nПериметр прямоугольника: " + rectangle.Perimeter);
        }
        else
        {
            //t3
            Point p1 = new Point(1, 1);
            Point p2 = new Point(1, 2);
            Point p3 = new Point(2, 3);
            Point p4 = new Point(3, 2);
            Point p5 = new Point(3, 1);

            Figure triangle = new Figure(p1, p2, p3);
            Figure tetragon = new Figure(triangle, p4);
            Figure pentagon = new Figure(triangle, p4, p5);
            triangle.Name = "треугольник";
            tetragon.Name = "четырехугольник";
            pentagon.Name = "пятиугольник";
            triangle.PerimeterCalculator();
            tetragon.PerimeterCalculator();
            pentagon.PerimeterCalculator();
        }

    }
}
