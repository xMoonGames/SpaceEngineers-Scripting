# SpaceEngineers-Scripting
tips and snippets.

Space engineers uses C# with custom namespaces.

API wiki at [spaceengineerswiki](https://www.spaceengineerswiki.com/Scripting_API_Documentation)

Good repository with tutorials at [MDK-SE](https://github.com/malware-dev/MDK-SE/wiki/Quick-Introduction-to-Space-Engineers-Ingame-Scripts)

---

## Default clean script that will re-run every 100 server ticks

```c#
public Program()
{
    Runtime.UpdateFrequency = UpdateFrequency.Update100;
}

public void Save()
{
}

public void Main(string argument, UpdateType updateSource)
{
}
```

## Snippets

### Get a block in grid by its name (in example its an LCD called 'LCD'):

```c#
var lcd = GridTerminalSystem.GetBlockWithName("LCD") as IMyTextPanel;
```

### Get all blocks in grid with same name (in example gets all blocks with name 'LCD'):

```c#
List<IMyTerminalBlock> lcds = new List<IMyTerminalBlock>();  
GridTerminalSystem.SearchBlocksOfName("LCD", lcds);
```

### Get all blocks in grid of a particular type (in example batteries):

```c#
List<IMyTerminalBlock> batteries = new List<IMyTerminalBlock>();  
GridTerminalSystem.GetBlocksOfType<IMyBatteryBlock>(batteries);
```

---

## Functions that can help your scripting

### Get block detailed info by the info name:

```c#
string getDetailedInfoValue(IMyTerminalBlock block, string name)    
{   
    string value = "";   
    string[] lines = block.DetailedInfo.Split(new string[] { "\r\n", "\n", "\r" }, StringSplitOptions.None);   
    for (int i = 0; i < lines.Length; i++)    
    {   
        string[] line = lines[i].Split(':');   
        if (line[0].Equals(name))    
        {   
            value = line[1].Substring(1);   
            break;   
        }   
    }   
    return value;   
}  
```

### Convert power string to int:

```c#
int getPowerAsInt(string text)    
{   
    if (String.IsNullOrWhiteSpace(text))    
    {   
        return 0;   
    }   
    string[] values = text.Split(' ');   
    if (values[1].Equals("kW"))    
    {   
        return (int) (float.Parse(values[0])*1000f);   
    }   
    else if (values[1].Equals("kWh"))    
    {    
        return (int) (float.Parse(values[0])*1000f);    
    }   
    else if (values[1].Equals("MW"))    
    {   
        return (int) (float.Parse(values[0])*1000000f);   
    }   
    else if (values[1].Equals("MWh"))    
    {    
        return (int) (float.Parse(values[0])*1000000f);    
    }   
    else    
    {   
        return (int) float.Parse(values[0]);   
    }   
    return 0;   
}
```
